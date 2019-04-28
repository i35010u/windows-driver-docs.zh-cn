---
title: 数字签名
description: 数字签名
ms.assetid: 637212b2-bc57-414b-9a06-07f79d9264f9
keywords:
- 驱动程序数据包数字签名 WDK
- 数据包数字签名 WDK
- 数字签名 WDK、 驱动程序包
- WDK、 驱动程序包签名
- 驱动程序签名 WDK、 驱动程序包
- 签署驱动程序 WDK、 驱动程序包
- 设备安装 WDK，数字签名
- 驱动程序签名 WDK
- 有关数字签名的证书 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ef6a69e6867bc6edddd97a624d4073b1066dad1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356048"
---
# <a name="digital-signatures"></a>数字签名


数字签名基于 Microsoft 公钥基础结构技术，基于 Microsoft [Authenticode](authenticode.md)与受信任的证书颁发机构 (Ca) 的基础结构结合使用。 验证码，基于行业标准，允许供应商，或*软件发布者*、 文件的集合进行签名 (如[驱动程序包](driver-packages.md)) 通过使用代码签名[数字证书](digital-certificates.md)CA 颁发。

Windows 使用有效的数字签名来验证以下各项：

-   该文件或文件的集合进行签名。

-   签名者是受信任。

-   身份验证签名者的证书颁发机构是受信任。

-   发布后对其未被更改的文件的集合。

例如，对于此签名过程[驱动程序包](driver-packages.md)涉及以下：

-   发布服务器获取*X.509 数字证书*从 CA。 验证码证书也称为*签名证书*。 签名证书是一组数据，用于标识发布服务器，并仅后已验证的发布服务器的标识由 CA 颁发。 CA 可以是 Microsoft CA、 第三方商业 CA 或企业 CA。

    用于签名的证书进行签名[编录文件](catalog-files.md)的驱动程序包或设置为[嵌入签名](embedded-signatures-in-a-driver-file.md)驱动程序文件中。 标识受信任的发行者和受信任的 Ca 的证书安装在[证书存储区](certificate-stores.md)的维护 Windows。

-   签名证书包含私钥和公钥，它被称为*密钥对*。 使用私钥进行签名的编录文件[驱动程序包](driver-packages.md)或驱动程序文件中嵌入签名。 公钥用于验证驱动程序包的目录文件的签名或签名的驱动程序文件中嵌入的。

-   若要签署编录文件或文件中嵌入签名，签名过程首先生成加密哈希，或*指纹*，该文件。 签名过程然后会使用私钥加密的文件指纹，并将指纹添加到文件。

    签名过程还将添加有关发布服务器和 CA 颁发的签名证书的信息。 数字签名添加到生成文件指纹时则不会处理该文件的节中的文件中。

-   若要验证的数字签名的文件，Windows 提取有关发布服务器和 CA 的信息，并使用公钥进行解密的加密的文件指纹。

    Windows 可接受的文件的完整性和真实性的发布服务器仅当满足以下条件：

    -   已解密的指纹匹配的文件的指纹。
    -   发布服务器的证书安装在[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。
    -   颁发的发布者证书的 CA 的根证书安装在[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)。

有关如何插即用 (PnP) 设备安装使用的数字签名的详细信息[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)，请参阅[数字签名和即插即用设备安装](digital-signatures-and-pnp-device-installation.md)。

有关 Microsoft 公钥基础结构技术、 代码签名和数字签名的详细信息，请参阅[代码签名简介](https://go.microsoft.com/fwlink/p/?linkid=104071)并[代码签名最佳做法](https://go.microsoft.com/fwlink/p/?linkid=68250)。

 

 





