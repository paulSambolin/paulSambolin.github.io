---
title: Secure E-Trade account with Symantec VIP on Yubikey
author: Paul Sambolin
date: 2021-02-06 13:00:00 -0500
categories: [Blogging, Tutorial]
tags: [technology security]
pin: true
---

[E-Trade](https://us.etrade.com/) and others use [Symantec VIP](https://vip.symantec.com/) for their most secure (hardware) multi-factor authentication methods. I'll show how to use a Yubikey to generate 6 digit codes identical to Symantec VIP hardware.  **[Yubikey OTP](https://developers.yubico.com/OTP/) is not supported by E-Trade.  Here we use the Yubikey's second key slot (long press) to store the Symantec VIP secret used to generate the 6 digit codes.  Yubikey OTP key in the first key slot (short press) is not modified**

## Motivation
I already own a [Yubikey 5c](https://www.yubico.com/product/yubikey-5c/) and didn't want to purchase a Symantec hardware key (additional costs, delays, and only available in USB A)

## Install Software
1. Don't over think the installs, reading instructions usually isn't necessary, just install the correct software for your operating systems
  - [Docker](https://docs.docker.com/get-docker/)
  - [Yubikey Manager](https://www.yubico.com/products/services-software/download/yubikey-manager/)

2. Download the code to your computer

```bash
# if you have git installed, run git clone in the terminal
git clone https://github.com/dlenski/python-vipaccess.git

# else open this link in internet browser to download zip.  Unzip files
https://github.com/dlenski/python-vipaccess/archive/master.zip
```

## Provision Symantec VIP secret
Using docker makes this easy.  Open a terminal window, navigate to the `python-vipaccess` directory.  Run the following commands to provision a secret

```bash
# Build the python-vipaccess Docker image
docker build . -t python-vipaccess

# Run the python-vipaccess Docker image to provision a type FT12 (hardware) type secret
docker run python-vipaccess provision -p -t FT12
```

The VIP Credential Id and VIP Secret are in the `otpauth` line of the output.  The id is `FT0123456789` and the secret is `EVX5G4UZ2DPC7SCUIQSA7VQBX4BFQMCG`
> 'otpauth://hotp/VIP%20Access:**FT0123456789**?secret=**EVX5G4UZ2DPC7SCUIQSA7VQBX4BFQMCG**&digits=6&algorithm=SHA1&image=https%3A%2F%2Fraw.githubusercontent.com%2Fdlenski%2Fpython-vipaccess%2Fmaster%2Fvipaccess.png&counter=1'

## Add Symantec VIP secret to Yubikey
1. Inset the Yubikey
2. Open Yubikey Manager, the Yubikey should be automatically detected
3. Navigate to `Applications` > `OTP`
![alt text](/assets/img/posts/2021-02-06-symantec-vip/Yubikey-01.png "Yubikey-home")

4. Click `Configure` for `Long Touch (Slot 2)`
![alt text](/assets/img/posts/2021-02-06-symantec-vip/Yubikey-02.png "Yubikey-slots")

5. Select `OATH-HOTP` as the credential type and click `Next`
![alt text](/assets/img/posts/2021-02-06-symantec-vip/Yubikey-03.png "Yubikey-type")

6. Copy the VIP secret from earlier (`EVX5G4UZ2DPC7SCUIQSA7VQBX4BFQMCG`) to the `Secret key` field.  Keep the default of `6` for `Digits`.  Click `Finish` to save the key to the Yubikey
![alt text](/assets/img/posts/2021-02-06-symantec-vip/Yubikey-04.png "Yubikey-secret")

7. Test the key at [vip.symantec.com](https://vip.symantec.com/).  Remember to `Long Touch` the Yubikey in order to use the second slot.  (Note: the `symantec` website only worked on my mobile devices)


## Register Yubikey with E-Trade
1. Login to [E-Trade](https://us.etrade.com/), and navigate to `Profile/Security Settings`
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-01.png "Etrade-settings")

2. Click `Manage two-factor authentication`
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-02.png "Etrade-mfa")

3. Click the text `No mobile device? Add a hardware token.` 
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-03.png "Etrade-devices")

4. Enter the Credential Id (example `FT0123456789`) in the `Serial number` field.  Select the `Personal access code` field and `Long Touch` the Yubikey to generate a 6 digit code.  (Optional) Enter a nickname for each unique Yubikey.  Click `Add authenticator`
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-04.png "Etrade-token")

5. Congrats! Click `Done` on the confirmation
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-05.png "Etrade-done")

## Managing Devices in E-Trade
Follow steps 1 & 2 under the previous section `Register Yubikey with E-Trade` to view your registered MFA devices
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-06.png "Etrade-manage")

## Logging into E-Trade
I highly suggest you test logging in with the new key immediately!  Contact E-Trade support with any issues!
![alt text](/assets/img/posts/2021-02-06-symantec-vip/ETrade-07.png "Etrade-login")

## Closing Advice
It is best practice to generate two Symantec VIP keys and load them onto seperate Yubikeys.  Register both Yubikeys with E-Trade and store one in a safe location.  Delete all traces of the secret from the computer.  The Yubikey should possess the only copy of the secret for true hardware level security.
