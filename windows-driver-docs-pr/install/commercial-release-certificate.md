---
title: 商业发布证书
description: 商业发布证书
keywords:
- 商业版证书 WDK
- 目录文件 WDK 驱动程序签名，商业发布证书
- 公共版本驱动程序签名 WDK，商业发布证书
- release 签名 WDK，商业发布证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0054ba1d8710dd9cee4e60b37d612be3db7c699
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782981"
---
# <a name="commercial-release-certificate"></a>商业发布证书

 > [!CAUTION] 
 > 从2021开始，大多数交叉证书都将开始过期。 这些交叉证书过期后，链接到这些交叉证书的代码签名证书将无法再创建新的内核模式数字签名。 这会影响 Windows 的所有版本。 有关详细信息，请参阅 [弃用软件发行者证书和商业发布证书](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)。
 
*商业发布证书* 是指发行者从受信任的第三方商业证书颁发机构获取的数字证书， (CA) ，它是 Microsoft 根证书计划的成员。 GTE 和 VeriSign，Inc. 是此类 Ca 的两个示例。 作为此程序成员的 CA 将验证申请人的身份和权利，然后颁发申请人用于签署其驱动程序的证书。 签名过程使用发布者的标识对驱动程序进行标记，可用于验证驱动程序自签名以来是否未被修改。

出于安全原因，不应使用用于对驱动程序进行签名以对驱动程序进行签名的数字证书。 你应获取用于发布签名和测试签名的单独数字证书。 有关如何管理数字证书的信息，请参阅 [管理数字签名或代码签名密钥](managing-the-digital-signature-or-code-signing-keys.md)。

按照 CA 提供的说明，了解如何在将用于签署驱动程序的计算机上获取和安装发布证书。

有关如何从 CA 获取数字证书的详细信息，请参阅 [Microsoft 根证书计划成员](/previous-versions/ms995347(v=msdn.10)) 网站。

 

