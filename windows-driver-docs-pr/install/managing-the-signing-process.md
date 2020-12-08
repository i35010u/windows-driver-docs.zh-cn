---
title: 管理签名过程
description: 管理签名过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a253b91b9ab51bce086d11ccfe9f0df1aad90e45
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790557"
---
# <a name="managing-the-signing-process"></a>管理签名过程


签署[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)或在驱动程序文件中嵌入签名的过程涉及以下活动。

### <a name="driver-signing-administration"></a>驱动程序签名管理

这通常由发行者的程序管理和软件发布服务处理，并包括以下主题：

-   [选择适当的签名类型](./digital-signatures-and-pnp-device-installation--windows-vista-and-late.md)

-   获取所需的 [发布证书](release-certificates.md) 或 [测试证书](./makecert-test-certificate.md)

-   [管理数字签名或代码签名密钥](managing-the-digital-signature-or-code-signing-keys.md)

### <a name="driver-development"></a>驱动程序开发

这通常由发行者的开发团队处理，并包括以下各项：

-   实现该驱动程序。

-   为内部测试创建签名的驱动程序包。 有关测试签名的信息，请参阅 [在开发和测试期间对驱动程序进行签名](./introduction-to-test-signing.md)。

-   为发布创建签名的驱动程序包。 有关如何为版本的驱动程序签名的信息，请参阅 [为公共版本签署驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)。

