# Incorrect Git CA Instructions

The instructions in `applications/git/git.md` are incorrect and potentially harmful. They will likely break `git`'s ability to communicate with standard remotes like GitHub and GitLab.

## The Problem

The instructions for both Windows and Mac/Linux suggest overwriting the existing `ca-bundle.crt` file with the new custom certificate. This is incorrect because it removes all of the existing public Certificate Authorities (CAs) from the bundle. This means that `git` will no longer trust any remote servers that use a standard, public CA.

### Windows

The `ac` command in PowerShell is an alias for `Add-Content`, which is correct. However, the description is misleading. It says to "update http.sslcainfo", which is not what the command does. The command appends to the file pointed to by `http.sslcainfo`. The instructions should be clarified to reflect this.

### Mac and Linux

The command `git config --global http.sslcainfo /path/to/your/custom_ca_bundle.pem` is the most dangerous. It tells `git` to use the custom certificate bundle as the *only* source of trusted certificates. This will break communication with any server using a standard, public CA.

## The Solution

The correct way to add a custom certificate to `git` is to append it to the existing `ca-bundle.crt` file. This can be done with the following commands:

### Windows

```powershell
$git_ca_bundle = git config --get http.sslcainfo
Get-Content -Path "/path/to/your/custom_ca_bundle.pem" | Add-Content -Path $git_ca_bundle
```

### Mac and Linux

```bash
cat /path/to/your/custom_ca_bundle.pem >> $(git config --get http.sslcainfo)
```

These commands will add the custom certificate to the existing bundle, allowing `git` to trust both the custom certificate and the standard, public CAs.
