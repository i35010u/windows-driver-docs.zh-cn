---
title: 商业测试证书
description: 商业测试证书
ms.assetid: cedceb0c-d39e-45e2-aa42-62cd7b8bed1c
keywords:
- 商业测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 129d758c802610ef4f8b7fb9ba2ce3128d0b5036
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733690"
---
# <a name="commercial-test-certificate"></a>商业测试证书

 > [!CAUTION] 
 > 从2021开始，大多数交叉证书都将开始过期。 这些交叉证书过期后，链接到这些交叉证书的代码签名证书将无法再创建新的内核模式数字签名。 这会影响 Windows 的所有版本。 有关详细信息，请参阅 [弃用软件发行者证书和商业发布证书](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)。
 
*商业测试证书*是指发行者从受信任的第三方商业证书颁发机构获取的数字证书， (CA) ，它是 Microsoft 根证书计划的成员。 GTE 和 VeriSign，Inc. 是此类 CA 的两个示例。

作为 Microsoft 根证书计划成员的 CA 将验证申请人的身份和权利，然后颁发申请人用于签署其驱动程序的证书。 签名过程使用发布者的标识对驱动程序进行标记，可用于验证驱动程序自签名以来是否未被修改。

商业测试证书与 [商业版](commercial-release-certificate.md)证书的证书类型相同。 然而，出于安全原因，不应使用用于对驱动程序进行测试签名的数字证书来签署 release 驱动程序。 你应获取用于发布签名和测试签名的单独数字证书。 有关如何管理数字证书的信息，请参阅 [管理数字签名或代码签名密钥](managing-the-digital-signature-or-code-signing-keys.md)。

按照 CA 提供的说明操作，了解如何获取证书并将其安装在要签署驱动程序的计算机上。

有关如何从 CA 获取数字证书的详细信息，请参阅 [Microsoft 根证书计划成员](/previous-versions/ms995347(v=msdn.10)) 网站。

 

