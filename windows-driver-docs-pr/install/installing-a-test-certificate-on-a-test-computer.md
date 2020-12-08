---
title: 在测试计算机上安装测试证书
description: 在测试计算机上安装测试证书
keywords:
- 测试证书 WDK
- 安装测试证书 WDK
- 测试签名驱动程序包 WDK，安装测试证书
- 证书存储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d2d6c7f6f7b726b19bb06d6d60b7d192bf5be6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839513"
---
# <a name="installing-a-test-certificate-on-a-test-computer"></a>在测试计算机上安装测试证书


必须将用于嵌入驱动程序文件中的签名和对[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)进行签名的[测试证书](./makecert-test-certificate.md)添加到 "[受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md)和 "[受信任的发布者" 证书存储](trusted-publishers-certificate-store.md)中。 可以使用 [**certmgr.msc**](../devtest/certmgr.md) 工具手动将测试证书添加到这些证书存储，如 [使用 Certmgr.msc 在测试计算机上安装测试证书](using-certmgr-to-install-test-certificates-on-a-test-computer.md)中所述。

你还可以将默认域策略配置为在域中的计算机上自动部署测试证书，如 [通过使用默认域策略部署测试证书](deploying-a-test-certificate-by-using-the-default-domain-policy.md)中所述。

 

