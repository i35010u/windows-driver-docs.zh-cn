---
title: 欺骗身份
description: 欺骗身份
ms.assetid: adc0b986-a8c2-45ce-a4d5-9d4d867603b5
keywords:
- 威胁建模 WDK 文件系统中，身份欺骗
- 安全威胁模型 WDK 文件系统中，身份欺骗
- 欺骗标识 WDK 文件系统
- 身份欺骗 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe71c0ab36a0922ce1fc23e784a9c217d555cf6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344433"
---
# <a name="spoofing-identity"></a>欺骗身份


## <span id="ddk_spoofing_identity_if"></span><span id="DDK_SPOOFING_IDENTITY_IF"></span>


身份欺骗的概念允许非特权的代码以使用其他人的标识，因此，其安全凭据。 例如，使用某种形式的密码机制的驱动程序受到此类攻击。 并非所有此类驱动程序有安全缺陷，但它们很容易受到基于身份欺骗的安全缺陷。 设计人员和驱动程序的实施者，需要评估安全漏洞的等级。

存在的欺骗标识其他更微妙示例。 例如，依赖于用于解密密钥的智能卡加密筛选器驱动程序容易受到物理电子欺骗攻击是，如果智能卡丢失或被盗。 因此，筛选器驱动程序可能会添加一些其他要求，如生物识别确认或密码，以防止这种类别的攻击。

尝试执行其自己的安全检查的驱动程序必须特别小心，以确保其安全检查期间使用正确的凭据。 如果不这样做可以轻松地为将允许发现它执行会显示为具有已完成的其他人，因为安全描述符是正确的操作的恶意用户欺骗攻击。

一般情况下，驱动程序是最佳设计和实现，如果它们充分利用操作系统，而不是构造其自身中的现有安全机制。 这可以尽量降低实现其中可能包含错误的潜在位置数。

 

 




