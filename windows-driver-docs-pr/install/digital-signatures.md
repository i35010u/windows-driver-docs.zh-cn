---
title: 数字签名
description: 数字签名
ms.assetid: 637212b2-bc57-414b-9a06-07f79d9264f9
keywords:
- 驱动程序包数字签名 WDK
- 包数字签名 WDK
- 数字签名 WDK，驱动程序包
- 签名 WDK，驱动程序包
- 驱动程序签名 WDK，驱动程序包
- 对驱动程序进行签名 WDK，驱动程序包
- 设备安装 WDK，数字签名
- 驱动程序签名 WDK
- 证书 WDK，关于数字签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c9bbd98af239fc7971a2086f92f75a8a15e1ec
ms.sourcegitcommit: 057b72e8a44ba8f4282e072edc7be0b7e9341d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412484"
---
# <a name="digital-signatures"></a>数字签名


数字签名基于 microsoft 公钥基础结构技术，它基于 Microsoft [Authenticode](authenticode.md) 与受信任证书颁发机构的基础结构的基础结构)  (CAs。 验证码（基于行业标准）允许供应商或*软件发布者*使用 CA 颁发的代码签名[数字证书](digital-certificates.md)对文件或文件集合进行签名 (如[驱动程序包](driver-packages.md)) 中。

Windows 使用有效的数字签名来验证以下各项：

-   文件或文件集合已签名。

-   签名者是受信任的。

-   对签名者进行身份验证的证书颁发机构是受信任的。

-   文件集合在发布之后未被更改。

例如， [驱动程序包](driver-packages.md) 的此签名过程涉及以下内容：

-   发布者从 CA 获取 *x.509 数字证书* 。 Authenticode 证书也称为 *签名证书*。 签名证书是用于标识发布者的一组数据，只有在 CA 验证了发布者的标识之后，CA 才能颁发该证书。 CA 可以是 Microsoft CA、第三方商业 CA 或企业 CA。

    签名证书用于签署驱动程序包的 [编录文件](catalog-files.md) 或在驱动程序文件中 [嵌入签名](embedded-signatures-in-a-driver-file.md) 。 标识受信任的发布者和受信任的 Ca 的证书安装在由 Windows 维护的 [证书存储](certificate-stores.md) 中。

-   签名证书包含私钥和公钥，这称为 *密钥对*。 私钥用于签署 [驱动程序包](driver-packages.md) 的编录文件或在驱动程序文件中嵌入签名。 公钥用于验证驱动程序包的目录文件的签名或嵌入驱动程序文件中的签名。

-   若要对目录文件签名或在文件中嵌入签名，签名过程首先会生成文件的加密哈希或 *指纹*。 签名过程随后使用私钥加密文件指纹，并将指纹添加到文件中。

    签名过程还会添加有关发布服务器和颁发签名证书的 CA 的信息。 将数字签名添加到文件的部分中，在生成文件指纹时不会处理该文件。

-   为了验证文件的数字签名，Windows 会提取有关发布者和 CA 的信息，并使用公钥对加密文件指纹进行解密。

    仅当满足以下条件时，Windows 才接受文件的完整性和发布者的真实性：

    -   解密的指纹与文件的指纹相匹配。
    -   发行者的证书安装在 " [受信任的发行者" 证书存储](trusted-publishers-certificate-store.md)中。
    -   颁发发行者证书的 CA 的根证书安装在 " [受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md)中。

有关即插即用 (PnP) 设备安装如何使用[驱动程序包](driver-packages.md)的 [目录文件](catalog-files.md)的数字签名的详细信息，请参阅[数字签名和 PnP 设备安装](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md)。

有关 Microsoft 公钥基础结构技术、代码签名和数字签名的详细信息，请参阅 [代码签名简介](https://go.microsoft.com/fwlink/p/?linkid=104071) 和 [代码签名最佳做法](https://go.microsoft.com/fwlink/p/?linkid=68250)。

 

 





