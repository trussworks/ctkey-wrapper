# ctkey-wrapper

`ctkey-wrapper` is a small bash script that runs the `ctkey` command and sets your
AWS environment variables to the key returned then runs the original command you
typed.

See [Getting started with Access Key CLI
tool](https://cloud.cms.gov/getting-started-access-key-cli-tool) for a link to
download the ctkey tool.

Download and unzip the ctkey file onto your local computer. Move the executable
that is applicable to your system (e.g., Mac/OS X) to a directory in your PATH.
Rename the executable to `ctkey`.

To verify things are working, run:

```shell
ctkey --version
```

Mac users: If you get an OS X error about the file not being trusted, go to
System Preferences > Security > General and click to allow ctkey.

Note: [Getting started with Access Key CLI
tool](https://cloud.cms.gov/getting-started-access-key-cli-tool) contains
additional instructions for using `ctkey`, but the `ctkey-wrapper` also
simplifies the usage.

The `ctkey-wrapper` could be used and adapted in multiple ways. One way is to
place the script in the `bin` directory of your infra repository:

```text
bin
├── aws -> ctkey-wrapper
├── ctkey-wrapper
└── terraform -> ctkey-wrapper
```

See
[terraform-layout-example](https://github.com/trussworks/terraform-layout-example)
for an example of how to structure the infra repository.

The `bin` directory typically contains an `aws-vault-wrapper` script with
symlinks for things like `aws`, `chamber`, `packer`, `terraform`, etc. depending
on the project's needs. `ctkey-wrapper` serves a similar purpose as the
`aws-vault-wrapper` on other project.

To use `ctkey-wrapper`, add the following environment variables to `.envrc` or
`.envrc.local`:

```shell
export CT_URL='https://cloudtamer.cms.gov/'
export CT_AWS_ROLE=<IAM_ROLE_NAME>
export CT_IDMS='2'
```

Add the following environment variables to your `.envrc.local`:

```shell
export CTKEY_USERNAME=<EUA ID>
export CTKEY_PASSWORD=<EUA PASSWORD>
```

The `AWS_ACCOUNT_ID` environment variable will also need to be set. In a
multi-account infra repository, set this in a `.envrc` file within each
account's subdirectory (dev, impl, prod, etc.).

Currently this also requires the user to be running the openconnect-tinyproxy
container [here](https://github.com/trussworks/openconnect-tinyproxy) to connect
to Cloudtamer.
