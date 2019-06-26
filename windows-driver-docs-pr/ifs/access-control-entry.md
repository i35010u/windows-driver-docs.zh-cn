---
title: 访问控制项
description: 访问控制项
ms.assetid: 4dc72f43-e5a7-441d-8586-f8893b9c1084
keywords:
- 安全描述符 WDK 文件系统，访问控制项
- 描述符 WDK 文件系统，访问控制项
- 访问控制条目 WDK 文件系统
- ACE WDK 的文件系统
- WDK 的文件系统的安全标识符
- Sid WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aad8e527a5c0517d6d6552cfaf4f19bfafdaf55d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381763"
---
# <a name="access-control-entry"></a>访问控制项


## <span id="ddk_access_control_entry_if"></span><span id="DDK_ACCESS_CONTROL_ENTRY_IF"></span>


访问控制项 (ACE) 介绍了与一个特定的 SID 相关联的访问权限。 访问控制项将评估操作系统以计算授予针对在其凭据时基于特定程序的有效访问权限。 例如，当用户登录到计算机，并执行程序，程序将使用与该特定用户的帐户关联的凭据。

因此，当程序尝试打开某个对象，Windows 将比较与对象关联的安全控制对该程序与关联的凭据。 安全引用监视器使用 ACE 信息来确定程序是否应允许或拒绝对给定对象的访问。 因此，ACE 确定安全子系统的行为。

下图说明了访问控制项。

![说明访问控制项的关系图](images/fssecurity-04.png)

有五种类型的 Ace 由安全子系统。 **类型**ACE 结构中的成员控制的 ACE 解释。 定义的类型包括：

-   **访问\_允许\_ACE\_类型**— 此类型表示的 ACE 指定将授予特定的 SID 的访问权限。

-   **访问\_DENIED\_ACE\_类型**— 此类型表示的 ACE 指定是要对其拒绝特定 sid 的访问权限。

-   **系统\_审核\_ACE\_类型**— 此类型表示的 ACE 指定审核行为。

-   **系统\_警报\_ACE\_类型**— 此类型表示的 ACE 指定警报的行为。

-   **访问\_允许\_复合\_ACE\_类型**— 此类型指示 ACE 绑定到特定服务器和正在模拟该实体。

因此，类型中的三个用于控制以编程方式访问一个对象，而其他两个用于控制安全子系统的审核和警报行为时访问的对象。 请注意，通过合并某些信息计算的安全子系统的实际行为或所有 Ace 与对象相关联。

驱动程序可能会构造的访问权限的访问控制项\_允许\_ACE\_类型使用该例程[ **RtlAddAccessAllowedAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtladdaccessallowedace)。 用于添加其他类型的 ACE 条目，驱动程序编写人员必须构造自己的函数，因为 WDK 不提供任何其他支持例程。

 

 




