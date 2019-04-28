---
title: 多会话复制保护
description: 多会话复制保护
ms.assetid: f6ac9854-3326-48da-9153-1eec596a157b
keywords:
- 复制保护 WDK 微型端口，多个会话
- 多个会话复制保护 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1c35ad31da613268a8b9a77de6ef7d01dbd5e22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345583"
---
# <a name="multiple-session-copy-protection"></a>多会话复制保护


## <span id="ddk_multiple_session_copy_protection_gg"></span><span id="DDK_MULTIPLE_SESSION_COPY_PROTECTION_GG"></span>


具有复制保护的设备的微型端口驱动程序可以根据需要支持多个同时进行的复制保护会话。 若要执行此操作，微型端口驱动程序应执行以下操作：

-   返回中的唯一复制保护键**dwCPKey**的每个复制保护激活。

-   保留所有会话已暂时都关闭之前，启用复制保护 (通过副总裁\_CP\_CMD\_更改) 或停用 (副总裁\_CP\_CMD\_停用)。 例如，微型端口驱动程序无法递增或递减引用计数，每次激活复制保护 (副总裁\_CP\_CMD\_激活) 或停用/已关闭，禁用复制保护时，才完全引用计数为零。

 

 





