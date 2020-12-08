---
title: 欺骗身份
description: 欺骗身份
keywords:
- 威胁模型 WDK 文件系统，哄骗标识
- 安全威胁模型 WDK 文件系统，哄骗标识
- 欺骗标识 WDK 文件系统
- 标识欺骗 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5cac39ad8868009282ab2d216599dbf9436e10d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839913"
---
# <a name="spoofing-identity"></a>欺骗身份


## <span id="ddk_spoofing_identity_if"></span><span id="DDK_SPOOFING_IDENTITY_IF"></span>


欺骗标识的概念是允许非特权代码使用其他人的标识，因此，它们的安全凭据。 例如，使用某种形式的密码机制的驱动程序受到此类攻击的限制。 并非所有此类驱动程序都具有安全缺陷，不过，它们容易遭受基于哄骗标识的安全缺陷。 驱动程序的设计人员和实施者需要评估漏洞的级别。

还有其他更微妙的欺骗性示例。 例如，如果智能卡丢失或被盗，则依赖于解密密钥的智能卡的加密筛选器驱动程序会遭受物理欺骗攻击。 因此，筛选器驱动程序可能会添加一些其他要求（例如生物识别确认或密码）来防范此类攻击。

尝试执行其自己的安全检查的驱动程序必须特别警惕，以确保它在安全检查过程中使用正确的凭据。 这样做可能会轻松地提供欺骗型攻击，使发现它的恶意用户能够执行其他人可能已完成的操作，因为安全描述符是正确的。

通常，如果驱动程序利用操作系统中现有的安全机制，而不是自行构造，则这些驱动程序的设计和实现是最佳的。 这会最大程度地减少实现可能包含错误的可能位置数。

 

 




