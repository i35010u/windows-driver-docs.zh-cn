---
title: 商业测试证书
description: 商业测试证书
ms.assetid: cedceb0c-d39e-45e2-aa42-62cd7b8bed1c
keywords:
- 商业测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b501a5421d958436c7415d8b02050c87b7580bf
ms.sourcegitcommit: 55171d00a4d0776ffbea40ab421f765c5432fcaa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995411"
---
# <a name="commercial-test-certificate"></a>商业测试证书

 > [!CAUTION] 
 > 从2021开始, 大多数交叉证书都将开始过期。 这些交叉证书过期后, 链接到这些交叉证书的代码签名证书将无法再创建新的内核模式数字签名。 这会影响 Windows 的所有版本。 有关详细信息, 请参阅[弃用软件发行者证书和商业发布证书](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)。
 
*商业测试证书*是指发行者从作为 Microsoft 根证书计划成员的受信任的第三方商业证书颁发机构 (CA) 获取的数字证书。 GTE 和 VeriSign, Inc. 是此类 CA 的两个示例。

作为 Microsoft 根证书计划成员的 CA 将验证申请人的身份和权利, 然后颁发申请人用于签署其驱动程序的证书。 签名过程使用发布者的标识对驱动程序进行标记, 可用于验证驱动程序自签名以来是否未被修改。

商业测试证书与[商业版](commercial-release-certificate.md)证书的证书类型相同。 然而, 出于安全原因, 不应使用用于对驱动程序进行测试签名的数字证书来签署 release 驱动程序。 你应获取用于发布签名和测试签名的单独数字证书。 有关如何管理数字证书的信息, 请参阅[管理数字签名或代码签名密钥](managing-the-digital-signature-or-code-signing-keys.md)。

按照 CA 提供的说明操作, 了解如何获取证书并将其安装在要签署驱动程序的计算机上。

有关如何从 CA 获取数字证书的详细信息, 请参阅[Microsoft 根证书计划成员](https://go.microsoft.com/fwlink/p/?linkid=16356)网站。

 

 





