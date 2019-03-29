---
title: 在测试计算机上安装测试证书
description: 在测试计算机上安装测试证书
ms.assetid: b28bd334-cd75-4ea1-8f1b-d9cd5b417b53
keywords:
- 测试证书 WDK
- 安装测试证书 WDK
- 测试签名驱动程序包 WDK，安装测试证书
- WDK 的证书存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa56bc6cf92ae4106d28cd3bfc61ea50a581a46a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562098"
---
# <a name="installing-a-test-certificate-on-a-test-computer"></a>在测试计算机上安装测试证书


[测试证书](test-certificates.md)用于在驱动程序文件中嵌入签名并进行签名[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)必须添加到[受信任根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)并[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。 您可以使用手动将添加一个测试证书到下列证书存储[ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)工具，如中所述[的测试计算机上安装测试证书的使用CertMgr](using-certmgr-to-install-test-certificates-on-a-test-computer.md).

您还可以配置要自动部署域中的计算机上的测试证书的默认域策略，如中所述[通过使用默认域策略部署测试证书](deploying-a-test-certificate-by-using-the-default-domain-policy.md)。

 

 





