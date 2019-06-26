---
title: Windows 内核模式执行支持库
description: Windows 内核模式执行支持库
ms.assetid: cfb8c6c0-9454-4dc6-98e8-c41cbf1c0cad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4bd2e7a9d6158937f2e66070d80ddf661e44b3ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358053"
---
# <a name="windows-kernel-mode-executive-support-library"></a>Windows 内核模式执行支持库


Windows 操作系统使用术语*executive 层*来指代内核模式组件，提供各种服务添加到设备驱动程序，包括：

-   对象管理

-   内存管理

-   进程和线程管理

-   输入/输出管理

-   配置管理

几个库一样，每个上述管理器提供直接的接口连接到其单独的技术。 但是，组合在一起作为 Executive 库通用接口的例程通常前缀为"**Ex**"，例如**ExGetCurrentResourceThread**。 Executive 库例程的列表，请参阅[Executive 库支持例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544582(v=vs.85))。

请注意 executive 层组件属于 Ntoskrnl.exe，但驱动程序和 HAL 不是管理层的层的一部分。

 

 




