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
ms.openlocfilehash: 416d58adf19d6e0e199f539e39b0b29c83167d45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383832"
---
# <a name="installing-a-test-certificate-on-a-test-computer"></a>在测试计算机上安装测试证书


[测试证书](test-certificates.md)用于在驱动程序文件中嵌入签名并进行签名[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)必须添加到[受信任根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)并[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。 您可以使用手动将添加一个测试证书到下列证书存储[ **CertMgr** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)工具，如中所述[的测试计算机上安装测试证书的使用CertMgr](using-certmgr-to-install-test-certificates-on-a-test-computer.md).

您还可以配置要自动部署域中的计算机上的测试证书的默认域策略，如中所述[通过使用默认域策略部署测试证书](deploying-a-test-certificate-by-using-the-default-domain-policy.md)。

 

 





