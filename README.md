# MauiIssue-WindowsCapabilities
This repository is an example for the issue https://github.com/dotnet/maui/issues/10287

### Reproduce on local machine

Open Powershell and navigate into the repo folder (after cloning the repo). Run the following command to build a certificat:
```
New-SelfSignedCertificate -Type Custom `
                          -Subject "CN=User Name" `
                          -KeyUsage DigitalSignature `
                          -FriendlyName "Maui Issue 9879 test Cert Windows" `
                          -CertStoreLocation "Cert:\CurrentUser\My" `
                          -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.3", "2.5.29.19={text}")
```
Now to build the x86 msix run:
```
dotnet publish TestIssue9879/MauiApplication/MauiApplication.csproj -c Release -f:net6.0-windows10.0.19041.0 /p:GenerateAppxPackageOnBuild=true /p:Platform=x86 /p:AppxPackageSigningEnabled=true /p:PackageCertificateThumbprint="<YOUR_THUMBPRINT>" /p:RuntimeIdentifier=win10-x86
```

To build the x64 msix run:
```
dotnet publish TestIssue9879/MauiApplication/MauiApplication.csproj -c Release -f:net6.0-windows10.0.19041.0 /p:GenerateAppxPackageOnBuild=true /p:Platform=x64 /p:AppxPackageSigningEnabled=true /p:PackageCertificateThumbprint="<YOUR_THUMBPRINT>"
```
