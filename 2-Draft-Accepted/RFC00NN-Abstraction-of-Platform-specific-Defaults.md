---
RFC: RFC00NN
Author: Joey Aiello
Status: Draft
Version: 0.1
Area: Module loading, built-in variables
Comments Due: 06/12/2017
Plan to implement: No (but someone on the PS Team should)
---

# Abstraction of Platform-specific defaults

This RFC discusses some possible solutions for dealing with platform differences in PowerShell when authoring scripts or modules.

## Motivation

Different platforms (e.g. Windows vs. Linux) have different default behaviors in order to enhance the local interactive and scripting experiences.
Some of these differences include:

- Certain GNU-like aliases traditionally included in Windows are not present on Linux
- File encodings will be different when the `Encoding` parameter is not specified for cmdlets which manipulate file contents
(see RFC0020 for more details)
- Paths are normalized to `\` on Windows and to `/` on Linux/macOS
- The `EditMode` for PSReadline is set to `Windows` on Windows and `Emacs` on macOS/Linux 
(this should not impact script/module scenarios but users may want to change their interactive defaults)

While not controlled by PowerShell, there are also differences exposed by various platforms which impact PowerShell.
Some of these differences include:

- Environment variables and most file systems on Linux/macOS are case-sensitive
(see PowerShell/PowerShell#3571)
- Binaries on Windows use the `exe` file extension; any file with the `+x` attribute on macOS/Linux can be executed

## Goals

First, it's important that all of these platform-specific defaults are accessible behind a single interface or namespace.
This allows them to be easily discovered by the end-user, and it makes any proposed mechanism for changing the defaults more maintainable.

Next, we should mitigate any problems that might arise from dynamic scoping of variables or states which control these modifiable behaviors.
For instance, an interactive user on Windows may want to run a script which changes to the Linux-based defaults that it requires.
After this script has finished executing, the user's interactive behavior should return back to Windows defaults.

For any of these modifiable defaults, we should also enable one-off overrides.
For instance, regardless of how the encoding defaults are set, the `-Encoding` parameter on a cmdlet should always be the last to win.
We should ensure that all modifiable defaults have overrides like this.

Lastly, many of these modifiable defaults already have mechanisms for changing behavior.
Whatever abstraction we expose for managing these values should respect and reflect the existing mechanisms.
For example, if I use the new mechanism for changing my PSReadline `EditMode`, `Get-PSReadlineOption` should reflect this change.

## Specification

To fulfill goal #2 above, we should create a parse-time construct so that a script can scope itself only to 

## Alternate Proposals and Considerations

### Use only a runtime construct

Instead of creating a parse-time construct for switching platform defaults, 