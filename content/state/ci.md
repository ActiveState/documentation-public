---
title: "Using State Tool on CI/CD"
weight: 4
---

To use the State Tool on CI you need to install and configure the State Tool to run without any prompting for paths or other information.

## Install without prompts

Our install scripts have the same usage on Linux(install.sh) and Windows(install.ps1):

```text
install.sh|install.ps1 [-b <branch>] [-n] [-f ] [-t <dir>] [-e <file>] [-h] [--activate]

Flags:
 -b <branch>          Specify an alternative branch to install from. Default: unstable
 -n                   Do not prompt for anything when installing into a new location
 -f                   Force overwrite. Overwrites the existing State Tool.
 -t <dir>             Install into target directory <dir>.
 -e <file>            Filename to use. The default name is `state`.
 --activate <project> Activate a project upon successful installation of the State Tool. For example: `--activate ActiveState/ActivePython-3.6`
 -h                   Shows usage information.
```

When installing for CI you will want to pass the `-n` flag to bypass any prompts and use default answers. You can further 
supplement this with the `-t` and `-e` flags to manually specify the target directory and executable name. You cannot use the `--activate` command in combination with the `-n` flag.

If you don't specify the `-t` or `-e` flags, the executable is named `state` and it is installed in `/usr/local/bin` (Linux) or `C:\Users\<username>\AppData\Roaming\ActiveState\bin\` (Windows).

Alternatively, you can use the force overwrite `-f` to ensure that any existing copy of the State Tool is replaced with the version you are installing.

### Example

Execute the following commands in your terminal to download the State Tool installation script and silently install the executable as `/opt/state_tool/state_cli.exe`.

```text
curl -O -s https://platform.activestate.com/dl/cli/install.sh
chmod +x install.sh
./install.sh -b master -n -t /opt/state_tool -e state_cli.exe
```

## Authenticate without prompts or passwords

The State Tool will use the following environment variables if they are defined:

- `ACTIVESTATE_API_KEY`: The API key to use for authentication (this is not sufficient if you're using secrets).
- `ACTIVESTATE_PRIVATE_KEY`: The private key to use for decrypting secrets.

### Obtaining the API Key

Currently, you can only generate an API Key by calling our API directly. You can use the following `curl` one liner:

```text
curl -X POST "https://platform.activestate.com/api/v1/apikeys" \
-H "accept: application/json" -H "Content-Type: application/json" \
-H "Authorization: Bearer `state export jwt`" \
-d "{ \"name\": \"APIKeyForCI\"}"
```

Notice the `APIKeyForCI` value, you are free to customize it to something more uniquely applicable to your use-case.

Also note that this command uses the State Tool to obtain the authentication token. You need to ensure that you run this from a terminal where the State Tool is installed and you are authenticated as the user for which you want to generate an API key.

### Obtaining the Private Key

Like the API Key you will need to use a terminal that has the State Tool installed, and the intended user authenticated.

Once authenticated, you can find the private key value at `<configdir>/activestate/cli-unstable/private.key`.

The configdir varies per platform, but in most cases will be at one of:

 - Windows: `%HOME%\AppData\Roaming\activestate\cli-unstable\`
 - Linux: `~/config/activestate/cli-unstable/`
 - macOS: `~/Library/Application\ Support/activestate/cli-unstable/`

The private key environment variable expects the actual private key value, not the filepath.

