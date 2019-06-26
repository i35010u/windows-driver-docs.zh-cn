---
title: 使用 CertMgr 在测试计算机上安装测试证书
description: 使用 CertMgr 在测试计算机上安装测试证书
ms.assetid: 5928c810-65e8-412e-9723-7b371574006c
keywords:
- Certmgr 工具
- 证书管理器工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b542250b705fdb4faaf1ac70e31d46b05089e7b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384772"
---
# <a name="using-certmgr-to-install-test-certificates-on-a-test-computer"></a>使用 CertMgr 在测试计算机上安装测试证书


若要使用的测试计算机上安装测试证书[ **CertMgr**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)，请执行以下步骤：

1.  将证书复制 ( *.cer*) 文件，这是用于[测试签名](test-signing-driver-packages.md)驱动程序，到测试计算机。 可以将证书文件复制到测试计算机上的任何目录。

2.  使用[ **CertMgr** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)命令以将证书添加到[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)和[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。

以下 CertMgr 命令将证书文件中添加证书*CertificateFileName.cer*到受信任的根证书颁发机构的证书存储在测试计算机上：

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine root /all
```

以下 CertMgr 命令将证书文件中添加证书*CertificateFileName.cer*到受信任的发行者的证书存储在测试计算机上：

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
```

 

 





