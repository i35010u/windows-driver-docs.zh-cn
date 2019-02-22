---
title: 商业测试证书
description: 商业测试证书
ms.assetid: cedceb0c-d39e-45e2-aa42-62cd7b8bed1c
keywords:
- 商用测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e0f00c371f7a939988eb837e6423d1bb0928f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543296"
---
# <a name="commercial-test-certificate"></a>商业测试证书


一个*商业测试证书*指的是发布服务器将从属于 Microsoft 根证书计划的受信任的第三方的商业证书颁发机构 (CA) 获取数字证书。 GTE 和 VeriSign，Inc.是这种 CA 的两个示例。

CA，则 Microsoft 根证书程序成员的验证的标识和授权的应聘者，然后颁发证书申请人用来签名的驱动程序。 签名过程具有发布者的标识标记的驱动程序，并可以用于验证该驱动程序签名后未被修改。

商业测试证书是相同类型的证书，因为[商业版本发布证书](commercial-release-certificate.md)。 但是，出于安全原因，您不应使用到测试签名驱动程序中用于还对版本驱动程序签名的数字证书。 你应获取单独使用版本签名证书和用于测试签名的数字证书。 有关如何管理电子证书的信息，请参阅[管理的数字签名或代码签名密钥](managing-the-digital-signature-or-code-signing-keys.md)。

按照如何获取并在计算机上安装证书的 CA 提供的说明将在其中登录驱动程序。

有关如何从 CA 获取数字证书的详细信息，请参阅[Microsoft 根证书程序成员](https://go.microsoft.com/fwlink/p/?linkid=16356)网站。

 

 





