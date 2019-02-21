---
title: 使用 CertMgr 测试计算机上安装测试证书
description: 使用 CertMgr 测试计算机上安装测试证书
ms.assetid: 5928c810-65e8-412e-9723-7b371574006c
keywords:
- Certmgr 工具
- 证书管理器工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccda7273b3b8173f0382a0e3e928fc6cb7a16193
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547458"
---
# <a name="using-certmgr-to-install-test-certificates-on-a-test-computer"></a>使用 CertMgr 测试计算机上安装测试证书


若要使用的测试计算机上安装测试证书[ **CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411)，请执行以下步骤：

1.  将证书复制 (*.cer*) 文件，这是用于[测试签名](test-signing-driver-packages.md)驱动程序，到测试计算机。 可以将证书文件复制到测试计算机上的任何目录。

2.  使用[ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)命令以将证书添加到[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)和[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。

以下 CertMgr 命令将证书文件中添加证书*CertificateFileName.cer*到受信任的根证书颁发机构的证书存储在测试计算机上：

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine root /all
```

以下 CertMgr 命令将证书文件中添加证书*CertificateFileName.cer*到受信任的发行者的证书存储在测试计算机上：

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
```

 

 





