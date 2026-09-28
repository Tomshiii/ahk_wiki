# Installation

## macOS

- Install [homebrew](https://brew.sh/) by opening the terminal and sending:

```c
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Windows
- Install [chocolatey](https://chocolatey.org/install) by performing the following;
> With `PowerShell`, you must ensure [`Get-ExecutionPolicy`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4) is not `Restricted`. We suggest using `Bypass` to bypass the policy to get things installed or `AllSigned` for quite a bit more security.
>
> Run an elevated powershell window and send;
> ```pwsh
> Get-ExecutionPolicy
>```
> If it returns `Restricted`, then run;
>```pwsh
> Set-ExecutionPolicy AllSigned
>```
> or
>```pwsh
> Set-ExecutionPolicy Bypass -Scope Process
>```
> Now run the following command:
> ```pwsh
> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
>```