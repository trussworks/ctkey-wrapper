# ctkey-wrapper

**Note:** As an initial approach, this script was copied from the EASi infra
repository to facilitate sharing across projects.

`ctkey-wrapper` is a small bash script that runs the `ctkey` command and sets your
AWS environment variables to the key returned then runs the original command you
typed.

See [Getting started with Access Key CLI
tool](https://cloud.cms.gov/getting-started-access-key-cli-tool) for a link to
download the ctkey tool.

Download and unzip the ctkey file onto your local computer. Move the Mac/OS X
executable to a directory in your PATH. Rename the executable to `ctkey`.

To verify things are working, run:

```shell
ctkey --version
```

If you get an OS X error about the file not being trusted, go to System
Preferences > Security > General and click to allow ctkey.

**Note:** Ignore the remaining setup instructions on the cloud.cms.gov page; the
`ctkey-wrapper` simplifies usage of the ctkey tool.

On EASi, we placed the `ctkey-wrapper` in the `bin` of our infra repository:

```text
bin
├── aws -> ctkey-wrapper
├── ctkey-wrapper
└── terraform -> ctkey-wrapper
```

The `bin` directory typically contains an `aws-vault-wrapper` script with
symlinks for things like `aws`, `chamber`, `packer`, `terraform`, etc. depending
on the project's needs. BUT we have replaced `aws-vault-wrapper` with
`ctkey-wrapper`.

Add the following environment variables to `.envrc` or `.envrc.local`:

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

Currently this also requires the user to be running the openconnect-tinyproxy
container [here](https://github.com/trussworks/openconnect-tinyproxy) to connect
to Cloudtamer.
