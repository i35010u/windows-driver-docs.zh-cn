---
title: Windows 内核模式执行支持库
description: Windows 内核模式执行支持库
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 68d983bd6f6f4edff8cc1e8df704d50561330b7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803723"
---
# <a name="windows-kernel-mode-executive-support-library"></a>Windows 内核模式执行支持库


Windows 操作系统使用术语 " *执行层* " 来指向设备驱动程序提供各种服务的内核模式组件，包括：

-   对象管理

-   内存管理

-   进程和线程管理

-   输入/输出管理

-   配置管理

上述每个管理器都向其各个技术提供直接接口，就像处理几个库一样。 但是，作为泛型接口分组到执行库中的例程通常带有 "**Ex**" 前缀，例如 **ExGetCurrentResourceThread**。 有关执行库例程的列表，请参阅 [执行库支持例程](/windows-hardware/drivers/ddi/_kernel/#executive-library-support-routines)。

请注意，执行层组件是 Ntoskrnl.exe 的一部分，但是该驱动程序和 HAL 不是执行层的一部分。

 

