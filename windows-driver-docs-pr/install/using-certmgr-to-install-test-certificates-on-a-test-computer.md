---
title: 使用 CertMgr 在测试计算机上安装测试证书
description: 使用 CertMgr 在测试计算机上安装测试证书
ms.assetid: 5928c810-65e8-412e-9723-7b371574006c
keywords:
- Certmgr.msc 工具
- 证书管理器工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51abb4b3bdcf80cd3b8ecb9c10454047d20f6d07
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097187"
---
# <a name="using-certmgr-to-install-test-certificates-on-a-test-computer"></a>使用 CertMgr 在测试计算机上安装测试证书


若要使用 [**certmgr.msc**](../devtest/certmgr.md)在测试计算机上安装测试证书，请执行以下步骤：

1.  将证书 (*.cer*) 文件（用于对驱动程序进行 [测试签名](test-signing-driver-packages.md) ）复制到测试计算机。 可以将证书文件复制到测试计算机上的任何目录中。

2.  使用 [**certmgr.msc**](../devtest/certmgr.md) 命令将证书添加到 " [受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md) 和 " [受信任的发布者" 证书存储](trusted-publishers-certificate-store.md)中。

以下 Certmgr.msc 命令将证书文件 *CertificateFileName* 中的证书添加到测试计算机上受信任的根证书颁发机构证书存储：

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine root /all
```

以下 Certmgr.msc 命令将证书文件 *CertificateFileName* 中的证书添加到测试计算机上的 "受信任的发行者" 证书存储：

```cpp
CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
```

 

