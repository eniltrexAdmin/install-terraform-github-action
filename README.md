# install-terraform-github-action
A git hub action to install terraform, by eniltrex.

The motivation behind that is that I tried to use this one:
https://github.com/marketplace/actions/install-terraform but it got stuck

I believe the main reason is that I had in my project already a directory called "terraform"
that's why it didn't work.

I realized that when doing this action that you are checking now.

When I realized that, instead of trying the above link again with the option "working-directory",
which would have been the obvious thing to do if I weren't an idiot, I just added a variable here to specify it.

Well now it's finished. So it doesn't hurt

I also took a look at this: https://github.com/hashicorp/setup-terraform, but my TL;DR conlcusion
of this one is that it is about terrafrom in the cloud and I am not using that, I believe?

## Usage

Make sure to use v1.0.3 at least or it will break.

```yaml
      - uses: actions/checkout@v2
      - id: EniltrexAction
        uses: eniltrexAdmin/install-terraform-github-action@v1.0.3
        with:
          version: '1.0.6'
          working-directory: 'install-terraform'
```

then you can execute terraform commands like those ones:

```yaml
    - name: Terraform apply
      run: |
          terraform init -backend-config="bucket=xxxx" \
             -backend-config="key=infrastructure/production/terraform.tfstate" \
             -backend-config="region=eu-xest-x"
          terraform plan -out=tfplan -input=false
          terraform apply  -input=false tfplan
```