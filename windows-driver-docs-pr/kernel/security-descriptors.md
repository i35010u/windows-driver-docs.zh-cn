---
title: 安全描述符
description: 安全描述符
keywords:
- 安全描述符 WDK 对象
- 系统 ACL WDK 对象
- SACL WDK 对象
- 自由 ACL WDK 对象
- DACL WDK 对象
- 访问控制列表 WDK 对象
- ACL WDK 对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8077d3316cc316791258b393cd967c4b9b9ae4bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829531"
---
# <a name="security-descriptors"></a>安全描述符


每个对象都有一个 *安全描述符*，其中包含对象的安全设置。 在内核模式下，不透明的 [**安全 \_ 描述符**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_security_descriptor) 数据类型表示安全说明符。

安全描述符中的信息存储在 (Acl) 的 *访问控制列表* 中。 访问控制列表由一系列 (Ace) 的 *访问控制项* 组成。

安全描述符有两个单独的 Acl：

-   *系统 ACL* (SACL) ，用于确定对对象记录的操作。

-    (DACL) 的 *自由 ACL* ，用于确定哪些用户可以对对象执行特定操作。

通常，驱动程序开发人员只关心任意 Acl。 有关系统 Acl 的详细信息，请参阅 Microsoft Windows SDK。

对于任意 ACL，每个 ACE 都包含三个信息片段：

-   SID)  (*安全标识符* 。 安全标识符确定 ACE 适用的内容。 SID 可以表示单个用户或一组用户。 例如，World SID 表示所有用户的集合。

-   一组访问权限。 有关访问权限的说明，请参阅 [访问权限](access-rights.md)。

-   授予或拒绝访问权限集。

对于驱动程序，最重要的安全描述符是驱动程序的设备对象的描述符。 有关详细信息，请参阅 [保护设备对象](controlling-device-access.md)。

有关一般安全描述符的详细信息，请参阅 Windows SDK。

 

