---
title: 管理数字签名或代码签名密钥
description: 管理数字签名或代码签名密钥
ms.assetid: 3aaa713b-c964-4a1e-9b2c-dee66cb4c4b2
keywords:
- 驱动程序签名 WDK，加密密钥
- 签名的驱动程序 WDK，加密密钥
- 数字签名 WDK，加密密钥
- 签名 WDK，加密密钥
- 加密 WDK 驱动程序签名
- 密钥 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 568f0568e9054f6b22a50707be718e94559c5c82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523483"
---
# <a name="managing-the-digital-signature-or-code-signing-keys"></a>管理数字签名或代码签名密钥


是的 Authenticode 签名过程核心的加密密钥必须保护且发布者的最有价值的资产那样悉心对待。 这些密钥表示组织的标识。 使用这些密钥签署的任何代码显示给 Windows 好像它包含可抵达组织的有效数字签名。 如果密钥被盗，它们可以用于通过欺骗手段签署恶意代码，而且可能会导致传递包含特洛伊木马的代码或病毒似乎来源于合法发行商。


 

 





