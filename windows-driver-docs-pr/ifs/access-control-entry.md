---
title: 访问控制项
description: 访问控制项
ms.assetid: 4dc72f43-e5a7-441d-8586-f8893b9c1084
keywords:
- 安全描述符 WDK 文件系统，访问控制项
- 描述符文件系统、访问控制项
- 访问控制入口 WDK 文件系统
- ACE WDK 文件系统
- 安全标识符 WDK 文件系统
- Sid WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eebdd3c308b1b5189ac9eeba239c859ca341c774
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066266"
---
# <a name="access-control-entry"></a>访问控制项


## <span id="ddk_access_control_entry_if"></span><span id="DDK_ACCESS_CONTROL_ENTRY_IF"></span>


 (ACE) 的访问控制项描述与特定 SID 关联的访问权限。 访问控制项由操作系统计算，以便根据其凭据计算授予特定程序的有效访问权限。 例如，当用户登录到计算机，然后执行程序时，该程序将使用与该特定用户帐户关联的凭据。

因此，当某个程序尝试打开某个对象时，Windows 会将与该程序关联的凭据与该对象关联的安全控件进行比较。 然后，安全引用监视器使用 ACE 信息来确定是否应允许或拒绝程序访问给定的对象。 因此，ACE 确定安全子系统的行为。

下图说明了访问控制项。

![说明访问控制项的关系图](images/fssecurity-04.png)

安全子系统使用了五种类型的 Ace。 ACE 结构的 **类型** 成员控制 ace 的解释。 定义的类型为：

-   **访问 \_允许的 \_ ACE \_ 类型**-此类型指示 ace 指定将授予特定 SID 的访问权限。

-   **访问 \_拒绝的 \_ ACE \_ 类型**-此类型指示 ACE 指定将拒绝特定 SID 的访问权限。

-   **系统 \_AUDIT \_ ACE \_ 类型**-此类型指示 ACE 指定审核行为。

-   **系统 \_警报 \_ ACE \_ 类型**-此类型指示 ACE 指定警报行为。

-   **访问 \_允许的 \_ 复合 \_ ACE \_ 类型**-此类型指示 ACE 与特定服务器以及它正在模拟的实体相关联。

因此，其中三个类型用于控制对对象的编程访问，而另两个类型用于控制访问对象时安全子系统的审核和警报行为。 请注意，安全子系统的实际行为是通过组合与对象关联的部分或全部 Ace 的信息来计算的。

驱动程序可以 \_ \_ \_ 使用例程 [**RtlAddAccessAllowedAce**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtladdaccessallowedace)构造访问权限允许的 ACE 类型的访问控制项。 为了添加其他类型的 ACE 条目，驱动程序编写器必须构造自己的函数，因为 WDK 不提供任何其他支持例程。

 

