# vpnctl

The `vpnctl` cli provides an automated way of connecting to VPN using
Cisco AnyConnect and RSA SecureID soft token.

## Getting Started
This guide is for `vpnctl` version 1.0. The version information can be found by running the following command `vpnctl -v` or `vpnctl --version`.

### Requirements
This `vpnctl` cli works only with the following requirement(s):
- Mac OS (tested on Catalina and Big Sur)
- Uses `AppleScript` for RSA Token automation
    - Hence it should have necessary permissions in `Security & Privacy`
- Cisco AnyConnect CLI `/opt/cisco/anyconnect/bin/vpn`
- Written in Bash + AppleScript

#### Limitations
And here goes the limitation(s):
- `vpnctl` is designed to work with the application based software token version. It doesn't work with email based on-demand token.


### Installation
The easiest way to install is - On your terminal run the following commands -

using curl

    ❯ curl -sSLO <>

or using wget

    ❯ wget -O vpnctl <>

you can now move the script to a executable path

    ❯ install vpnctl /usr/local/bin

you are good to go.

#### Note:

As the script contains AppleScript which interacts with the RSA Token Software
on your macOS -- proper permissions needs to be provided in the `Security & Privacy`.
- Open `Security & Privacy` from `System Preferences`
- Go to `Privacy`
- Unlock to make changes by clicking on `Click the lock to make changes` on the bottom left corner of the window.
- Under `Accessibility`
    - Tick `iTerm` or `Terminal` (or your preffered terminal) and `Script Editor`
- Under `Automation`
    - Under `iTerm` or `Terminal`
        - `SecureID` and `System Events` must be selected.
    - This option maybe already selected if you have accepted the permission prompt from the terminal.
> If you don't see those mentioned options in the list -- you may need to run `vpnctl connect` once to trigger those permission warnings first.


### Usages

#### Initial Configuration
The cli requires an initial configurations to be set in order to use it. The initial
settings can be set by running `vpnctl configure` command.

- Upon running the `vpnctl configure` command you will be prompted to enter your username with the default being pickedup and shown in `[DEFAULT_USERNAME]` -- incase you
want to go with the default just click enter and skip the username prompt.
- Then
will be asked to enter your `RSA Pin` which is a `4 digit` pin you use in your
`RSA Software` to get a token. It's safe to enter `RSA Pin` as `vpnctl` uses masOS's builtin <b>keychain manager</b> to store the pin.
- Then select a preferred VPN server. Usually the closest one based on your location.

Here goes an example (this is a onetime setup).


    ❯ vpnctl configure
    Username [amitauddy]: amitauddy
    RSA Pin:
    VPN Server >
    0: vpn-1.company.com	[default]
    1: vpn-2.company.com
    Select: 1

> Note: RSA Pin is not echoed on the screen. Don't get confused while entering.

#### Basic Commands
You are run the following commands in order to connect from the VPN.

    ❯ vpnctl connect
    Connecting to vpn-2.company.com.
    Passcode:
    Connected to vpn-2.company.com.

> Note: `vpnctl connect` will automatically switch your window for a moment to copy the RSA Token using AppleScript.

to disconnect

    ❯ vpnctl disconnect
    VPN disconnected.

to check the status
    ❯ vpnctl status
    VPN is currently disconnected.

and to check the version using the cli
    ❯ vpnctl --version
    1.0

for help message

    vpnctl provides an easy and automated way of connecting to VPN using Cisco
    AnyConnect and RSA SecureID soft token.

    Usage:
    vpnctl <command>
    vpnctl [options]

    Available Commands:
    configure  One time configuration command that sets the vpnctl settings. If this
               command is run with no arguments, you will be prompted for configuration
               values such as your username, rsa pin and preferred vpn host.

    connect    Helps connecting to VPN server.

    status     Helps checking the connection status.

    disconnect Helps disconnecting from the VPN server.

    Options:
    -h, --help    help for vpnctl
    -v, --version shows the version for vpnctl

### Common Errors
Sometime you will get some errors asking you to retry. Please go-ahead and retry -- that fixes the problem most of the time. You may also want to verify the whether the proper permissions are given as mentioned above.

    ❯ vpnctl connect
    330:338: execution error: SecurID got an error: Connection is invalid. (-609)
    Error: Something went wrong. Try connecting manually this time.

## More Resources
- https://developer.apple.com/library/archive/documentation/AppleScript/Conceptual/AppleScriptLangGuide/introduction/ASLR_intro.html
