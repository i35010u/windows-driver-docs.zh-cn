---
title: 使用 CertMgr 在测试计算机上安装测试证书
description: 使用 CertMgr 在测试计算机上安装测试证书
keywords:
- Certmgr.msc 工具
- 证书管理器工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b8c0d1b9a629792a8ed5c26c098499f88df0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805441"
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

 

