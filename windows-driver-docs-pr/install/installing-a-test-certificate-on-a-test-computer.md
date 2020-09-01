---
title: 在测试计算机上安装测试证书
description: 在测试计算机上安装测试证书
ms.assetid: b28bd334-cd75-4ea1-8f1b-d9cd5b417b53
keywords:
- 测试证书 WDK
- 安装测试证书 WDK
- 测试签名驱动程序包 WDK，安装测试证书
- 证书存储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e056f109623b90cd9ddc0c1633ae44d296fe5505
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097277"
---
# <a name="installing-a-test-certificate-on-a-test-computer"></a>在测试计算机上安装测试证书


必须将用于嵌入驱动程序文件中的签名和对[驱动程序包的](driver-packages.md) [目录文件](catalog-files.md)进行签名的[测试证书](./makecert-test-certificate.md)添加到 "[受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md)和 "[受信任的发布者" 证书存储](trusted-publishers-certificate-store.md)中。 可以使用 [**certmgr.msc**](../devtest/certmgr.md) 工具手动将测试证书添加到这些证书存储，如 [使用 Certmgr.msc 在测试计算机上安装测试证书](using-certmgr-to-install-test-certificates-on-a-test-computer.md)中所述。

你还可以将默认域策略配置为在域中的计算机上自动部署测试证书，如 [通过使用默认域策略部署测试证书](deploying-a-test-certificate-by-using-the-default-domain-policy.md)中所述。

 

