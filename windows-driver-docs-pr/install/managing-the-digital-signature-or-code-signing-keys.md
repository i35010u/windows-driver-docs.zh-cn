---
title: 管理数字签名或代码签名密钥
description: 管理数字签名或代码签名密钥
keywords:
- 驱动程序签名 WDK，加密密钥
- 为驱动程序签名 WDK、加密密钥
- 数字签名 WDK，加密密钥
- 签名 WDK，加密密钥
- 加密 WDK 驱动程序签名
- 密钥 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5049e3d10b69ee417e0ad86218f520b47fda1105
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834503"
---
# <a name="managing-the-digital-signature-or-code-signing-keys"></a>管理数字签名或代码签名密钥


验证码签名过程核心的加密密钥必须受到良好保护，并与发布者最有价值的资产进行处理。 这些密钥表示组织的标识。 使用这些密钥签署的任何代码都显示给 Windows，就好像它包含可抵达组织的有效数字签名一样。 如果密钥被盗，它们可能会被用来欺诈恶意代码，并可能导致传递包含特洛伊木马的代码或看似来自合法发行者的病毒。


 

 





