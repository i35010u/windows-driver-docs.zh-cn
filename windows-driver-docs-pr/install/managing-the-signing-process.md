---
title: 管理签名过程
description: 管理签名过程
ms.assetid: 80a1986f-1508-49c1-aec5-7084edff9485
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0699ad75e4f84375edef52a1d32f63c1d2e6e673
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106202"
---
# <a name="managing-the-signing-process"></a>管理签名过程


签署 [驱动程序包的](driver-packages.md) [目录文件](catalog-files.md) 或在驱动程序文件中嵌入签名的过程涉及以下活动。

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

