# qlik-cli

**qlik-cli**, known on the command line simply as qlik, is a CLI generated directly from API specifications. It is meant to be used for basically any task against Qlik Sense SaaS.

The project will be open-sourced in the near future. Until then however, this repo will serve as a placeholder and a mirror for releases.

For more information you can go to:
 * https://qlik.dev/tutorials/get-started-with-qlik-cli
 * https://qlik.dev/libraries-and-tools/qlik-cli

## Install

After any installation, don't forget to add the [completion](#completion) as well, it is usually quite helpful when writing commands.

### Brew

To install with brew you need to first tap our [qlik-oss/taps](https://github.com/qlik-oss/homebrew-taps) if you haven't already:
```
brew tap qlik-oss/taps
```
After the tap has been tapped you can install the tool with:
```
brew install qlik-cli
```
Just like that. :beers:

**Note:** This will work perfectly fine for either Mac or Linux (where you can use `linuxbrew`) and even Windows Subsystem Linux (WSL) as a matter of fact.

### Chocolatey

Want to install using Chocolatey? Then simply type:
```
choco install qlik-cli --source https://www.nuget.org/api/v2
```
And you're ready to go. :chocolate_bar:

If you want, you can add `nuget.org` as a source:
```
choco source add --name nuget.org --source https://www.nuget.org/api/v2
```
This way, you don't have to specify the source every time you want to install or upgrade `qlik-cli`.

**Note:** Check out the [Completion for Powershell](#completion-for-powershell) section if you're interested in how to set up Powershell completion.

### General

If you prefer not using any of the package managers above you can go to our [releases](https://github.com/qlik-oss/qlik-cli/releases) and choose a one suitable for your OS.

## Usage

The first step we recommend is to source the completion (see the section below).
After that, you will probably want to create a context with the command:
```
qlik context init
```
This will prompt you for an URL to your QCS tenant and then help you a bit on the way to generate an *API-key* to be used against your tenant. Your user will need to have the *developer role* and that *API-keys are enabled on your tenant* for this to work. 

After your context is set up, you are free to explore all the public APIs of QCS through `qlik`. If you think there's something missing, just let us now.

Last thing. As in the true spirit of any CLI, the documentation (in the extent it exists) is incorporated in `qlik`.
You can always add the `--help` flag to see the full documentation of any command.

### Completion

`qlik` provides auto completion of commands and flags for `bash`, `zsh` and `ps`. To load completion in your shell you can write the following snippet:
```
. <(qlik completion <shell>)
```
where shell should be one of `bash`, `zsh` or `ps`. You can also add this to your shell profile, e.g. `~/.bashrc` or `~/.zshrc`, if you want to include completion on startup (recommended). A robust way of doing so is the following:

```bash
if [ $(which qlik) ]; then
  . <(qlik completion <shell>)
fi
```
**Note:** Auto completion requires `bash-completion` to be installed on bash and zsh.

If you want add an alias for `qlik`, you can add the following snippet into your `rc` file aswell
```bash
alias <myalias>=qlik
complete -o default -F __start_qlik <myalias>
```
where `<myalias>` should be substituted for whatever you wish to call `qlik` as.

### Completion for Powershell

There is some completion support for Powershell although not to the same standard as for `bash`/`zsh`.
If you want to use it, you need to create a *Powershell profile*. If you don't have one you can run the following to create an empty profile:
```powershell
if ( -not (Test-Path $PROFILE) ) {
  echo "" > $PROFILE
}
```
When you have a profile **and** installed `qlik-cli`, add the following snippet to your profile:
```powershell
qlik completion ps > "./qlik_completion.ps1" # Create a file containing the powershell completion.
. ./qlik_completion.ps1                      # Source the completion.
```
The last thing you have to do is to *restart* the shell, after that the completion is installed.

You can verify it by typing:
```
qlik <tab>
```
If you have any questions or ideas on what could/should be improved, just reach out to us!

## Third-party dependencies

Third-party dependencies of the tool can be found [here](third-party-dependencies.md).

