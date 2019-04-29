---
title: 安全描述符
description: 安全描述符
ms.assetid: a5edd5e8-6fc7-4ab0-aebc-f0cd8e9299b6
keywords:
- 安全描述符 WDK 对象
- 系统 ACL WDK 对象
- SACL WDK 对象
- 自由 ACL WDK 对象
- DACL WDK 对象
- WDK 对象的访问控制列表
- ACL WDK 对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d2e9fc52a04ba5c3d3363750fb3e0964249e74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377291"
---
# <a name="security-descriptors"></a>安全描述符


每个对象具有*安全描述符*，其中包含一个对象的安全设置。 在内核模式下不透明[**安全\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563689)数据类型表示的安全描述符。

安全描述符中的信息存储在*访问控制列表*(Acl)。 访问控制列表组成的一系列*访问控制项*(Ace)。

安全描述符具有两个单独的 Acl:

-   一个*系统 ACL* (SACL)，用于确定将记录对某个对象的操作。

-   一个*自由 ACL* (DACL)，用于确定哪些用户可以执行对象上的特定操作。

通常情况下，驱动程序开发人员才关心的自定义 Acl。 有关系统 Acl 的详细信息，请参阅 Microsoft Windows SDK。

对于自定义 ACL，每个 ACE 包含三个信息片段：

-   一个*安全标识符*(SID)。 安全标识符确定谁 ACE 所应用到。 单个用户或一组用户，可以表示一个 SID。 例如，世界 SID 表示的所有用户的组。

-   一组访问权限。 访问权限的说明，请参阅[访问权限](access-rights.md)。

-   组访问权限是授予，还是被拒绝。

驱动程序，最重要的安全描述符是那些用于驱动程序的设备对象。 有关详细信息，请参阅[保护设备对象](securing-device-objects.md)。

详细了解安全描述符一般情况下，请参阅 Windows SDK。

 

 




