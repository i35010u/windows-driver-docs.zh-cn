---
title: Windows 内核模式执行支持库
description: Windows 内核模式执行支持库
ms.assetid: cfb8c6c0-9454-4dc6-98e8-c41cbf1c0cad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9464743c547600021b7a9dc7ef74d1624ab4d369
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184247"
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

 

