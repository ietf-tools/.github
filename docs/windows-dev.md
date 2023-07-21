# IETF Tools development on Windows

While most projects can run in a docker container on Windows, you'll likely encounter various issues and performance limitations by doing so. It's recommended to instead develop in [WSL2](https://docs.microsoft.com/en-us/windows/wsl/) (Windows Subsystem for Linux) which enables you to run a full Linux system directly on Windows.

## Requirements

- Windows 10 version 2004 and higher (Build 19041 and higher), or Windows 11
- Virtualization enabled on your machine
- [Docker Desktop](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)

**Optional but recommended**

- [Windows Terminal](https://aka.ms/terminal)
- [Visual Studio Code](https://code.visualstudio.com/), with the **WSL** and **Dev Containers** extensions

## Install WSL2 (Windows Subsystem for Linux)

> Instructions taken from [https://docs.microsoft.com/en-us/windows/wsl/install](https://docs.microsoft.com/en-us/windows/wsl/install)

In an **administrator** PowerShell or Command Prompt, run the following command and then restart your machine:

```powershell
wsl --install
```

This command will enable the required optional components, download the latest Linux kernel, set WSL 2 as your default, and install the default Ubuntu distribution.

The first time you launch a newly installed Linux distribution, a console window will open and you'll be asked to wait for files to de-compress and be stored on your machine. All future launches should take less than a second.

> Note that you can install any other Linux distro afterwards from the Microsoft Store.

## Run WSL for the first time

You can either:
- use **Windows Terminal** *(recommended)* and select **Ubuntu** in the dropdown list
- from a **Powershell** / **Command Prompt**, type `wsl.exe`
- from the Start Menu, click on the linux distribution you installed (e.g. Ubuntu)

You'll be prompted to choose a username and password the first time.

## Enable Docker Integration

In order to use Docker inside WSL2, we need to enable Docker integration in Desktop Desktop.

1. Open **Docker Desktop** and go to **Settings**.
2. Under the **Resources** > **WSL Integration** tab, make sure that `Enable integration with my default WSL distro` is enabled. If you installed additional distros from the Microsoft Store, make sure to enable them as well.
3. Click **Apply & Restart**

## Clone a project in WSL2

In WSL2, create a directory for your projects, under your home folder, e.g.:

```sh
mkdir projects
cd projects
```

Then clone the project of your choice at that location, e.g. for datatracker:

```sh
git clone https://github.com/ietf-tools/datatracker.git
```

## Open the project in VS Code

Navigate to the project folder and run `code .`, e.g.:
```
cd datatracker
code .
```

This will launch VS Code installed on your host and open the folder residing in WSL2.

From there, you can re-open the project in a devcontainer by typing <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>P</kbd>, then typing `reopen` and select **Dev Containers: Reopen in Container**. 
