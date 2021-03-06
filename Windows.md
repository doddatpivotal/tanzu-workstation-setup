# Windows Tanzu Workstation Setup

The following cheatsheet supports applications and utilities helpful for developer and operations (might I say devops) team members working with Tanzu.

The apps listed collected and used form a completely fresh Windows workstation.  See notes on creating the Windows 10 VM at the bottom.

## Applications and Utilities

Chrome - https://www.google.com/chrome

Install Git - https://git-scm.com/download/win

Install VS Code - https://code.visualstudio.com/download
- Enable auto save (File->Auto Save)
- Add the Kubernetes extension from Microsoft

Install Windows Subsystem for Linux 2 - https://docs.microsoft.com/en-us/windows/wsl/wsl2-kernel
- Steps 1-5

Install Docker - https://docs.docker.com/docker-for-windows/install/

Download Tanzu Kubernetes Grid Packages - https://www.vmware.com/go/get-tkg
- tanzu cli
  - Extract using 7-zip and copy tkg and Carvel utilities to ~/bin renaming them to name.exe
- kubectl cli
  - Extract using 7-zip and copy kubectl.exe to ~/bin
- ova's
- tkg extensions

Create single directory to put command line utilities into your path
- Create %USERPROFILE%/bin directory
- Add %USERPROFILE%/bin to path
  - Enter env in search bar, to launch the windows System Environment Variables dialog

Create a directory in your home for various git projects.  This is one of them.
- Create %USERPROFILE%/workspace
- git clone https://github.com/doddatpivotal/windows-tanzu-workstation.git
- Open VS Code to that directory
- Set Git Bash as default terminal

The following can be retrieved using Git BASH...

```bash
curl -L -o ~/bin/ytt.exe https://github.com/k14s/ytt/releases/download/v0.30.0/ytt-windows-amd64.exe
curl -L -o ~/bin/kapp.exe https://github.com/k14s/kapp/releases/download/v0.34.0/kapp-windows-amd64.exe
curl -L -o ~/bin/kbld.exe https://github.com/k14s/kbld/releases/download/v0.26.0/kbld-windows-amd64.exe
curl -L -o ~/bin/pivnet.exe https://github.com/pivotal-cf/pivnet-cli/releases/download/v3.0.0/pivnet-windows-amd64-3.0.0
curl -L -o ~/bin/yq.exe https://github.com/mikefarah/yq/releases/download/4.6.1/yq_windows_amd64.exe
curl -L -o ~/bin/tmc.exe https://tmc-cli.s3-us-west-2.amazonaws.com/tmc/0.2.1-ded34d75/windows/x64/tmc.exe
curl -L -o ~/bin/jq.exe https://github.com/stedolan/jq/releases/download/jq-1.6/jq-win64.exe
curl -L -o ~/bin/kind.exe https://kind.sigs.k8s.io/dl/v0.9.0/kind-windows-amd64

curl -LO https://get.helm.sh/helm-v3.4.0-rc.1-windows-amd64.zip
unzip helm-v3.4.0-rc.1-windows-amd64.zip 
mv windows-amd64/helm.exe ~/bin/helm.exe
rm helm*
rm -rf windows-amd64/

curl -LO https://github.com/vmware-tanzu/octant/releases/download/v0.16.1/octant_0.16.1_Windows-64bit.zip
unzip octant_0.16.1_Windows-64bit.zip
mv octant_0.16.1_Windows-64bit/octant.exe ~/bin/octant.exe
rm -rf octant_0.16.1_Windows-64bit
rm octant*

curl -LO https://github.com/buildpacks/pack/releases/download/v0.15.1/pack-v0.15.1-windows.zip
unzip pack-v0.15.1-windows.zip
mv pack.exe ~/bin/
rm pack*

curl -LO https://github.com/vmware/govmomi/releases/download/v0.23.0/govc_windows_amd64.exe.zip
unzip govc_windows_amd64.exe.zip
mv govc_windows_amd64.exe ~/bin/govc.exe
rm govc_win*

curl -LO https://github.com/concourse/concourse/releases/download/v6.7.5/fly-6.7.5-windows-amd64.zip
unzip fly-6.7.5-windows-amd64.zip
mv fly.exe ~/bin/fly.exe
rm fly-6.7.5*

# Goto https://network.pivotal.io and register for an account if you have not done so already.  Then grab the legacy api token for your profile and use that to login with the command below
pivnet login
pivnet download-product-files --product-slug='build-service' --release-version='1.1.1' --product-file-id=883033 --download-dir ~/bin
mv ~/bin/kp-windows-0.2.0.exe ~/bin/kp.exe

```

## Helpful Additions

Install WinSCP - https://winscp.net/eng/download.php

Install 7-zip - https://www.7-zip.org/

Windows Terminal - Install from Microsoft Store
- Search and then install
- Edit settings to add Git Bash as option: {"name": "Git Bash","commandline": "C:\\Program Files\\Git\\bin\\bash.exe","hidden": false}

>Note: If you don't have (and can't add Microstoft Store Extension) this site can be used to obtain direct link to the software: https://store.rg-adguard.net/

Install Python - Install from Microsoft Store
- Search and then install
- Note: Only seems to work in powershell

Install HTTPie
- Depends on Python
```bash
# From powershell window
pip install --upgrade pip setuptools
pip install --upgrade httpie
```
- Output of the above will suggest that you add a directory to your PATH variable.  After you so, you will be able to use HTTPie from powershell and GitBash


Install JDK - https://adoptopenjdk.net/releases.html
    JDK 11, Windows x86, msi
    In the installer choose to set JAVA_HOME variable

## Create Windows 10 Virtual Machine (Optional)

- Get Windows 10 ISO: https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise
- Using the windows server jumpbox, upload the ISO to vCenter
- Create new VM, Win 10 64-bit
  - 4 core, 16 GB RAM, 200 GB Disk
  - Under CPU choose "Expose hardware assisted virtualization to the guest OS"
- Boot VM from ISO disk and run through setup.  Use domain account.  USERNAME / PASSWORD
- Install VM Tools
- Set IP to address in static range
- Enable remote access: https://networking.grok.lsu.edu/Article.aspx?articleid=18609
- Now Remote Desktop to IP address
