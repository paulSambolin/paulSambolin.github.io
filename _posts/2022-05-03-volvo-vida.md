---
title: Volvo VIDA on VirtualBox
author: Paul Sambolin
date: 2022-05-03 13:00:00 -0500
categories: [Blogging, Tutorial]
tags: [technology security]
pin: true
---

Volvo VIDA is manufacturer level software for Volvo cars to read diagnostic codes and cusomtize vehicle settings.  I'll show how to get Volvo VIDA running on a windows laptop (windows is required to execute the `.exe` file which downloads the VirtualBox image)

## Motivation
My brother owns a 1999 Volvo s80 and while out driving it lit the check engine light and began shaking the whole car.  My Autel scanner could not read the diagnostic codes, so Volvo VIDA is required

## Install Software
1. Don't over think the installs
  - [VirtualBox](https://www.virtualbox.org/)
  - [Volvo Diag VirtualBox Image](https://volvodiag.com/product/virtualbox-build/)

2. Purchase the volvo vida 2014D adapter.  I paid $80 on amazon but the item has been purged from that site.  It is still available on Ebay and AliExpress for 90-200 [here](https://www.aliexpress.com/item/1005004068666318.html?_randl_currency=USD&_randl_shipto=US&src=google&aff_fcid=32e5b77bf467438f8dbd225af1015c96-1651507194375-00779-UneMJZVf&aff_fsk=UneMJZVf&aff_platform=aaf&sk=UneMJZVf&aff_trace_key=32e5b77bf467438f8dbd225af1015c96-1651507194375-00779-UneMJZVf&terminal_id=0116294380424ee2ab268cf4f55adb0b&afSmartRedirect=y)

## Import the image into VirtualBox and Run the Virtual OS
Follow this [youtube video](https://www.youtube.com/watch?v=dRf2tHAe8uQ) from the creator of the image

## Scan Vehicle
Start Car, plug adapter into car, plug adapter into laptop, ensure adapter is visible to the Virtual OS and the driver for the adapter gets installed

## Diagnose
This photo shows there is a misfire on cylinder 6
![alt text](/assets/img/posts/2021-02-06-symantec-vip/Yubikey-04.png "Yubikey-secret")

I swapped the coil packs between cylinder 6 and 5, then re-scanned the vehicle.  The diagnostic code now shows current on coil 5 and previous on cylinder 6 (missed a photo).  I installed a new [coil pack](https://www.amazon.com/Bosch-0221604008-Ignition-Coil-Plug/dp/B0048E10OY) for $50, cleared the diagnostic codes and went for a drive!

## Closing Advice
I have diagnosed and replaced coil packs on other vehicles so this was a straightforward repiar.  The hard part in the past was the Volvo VIDA software configuration.  Spending $5 on the image from volvodiag.com was well worth it
