---
title: Windows 内核模式执行支持库
description: Windows 内核模式执行支持库
ms.assetid: cfb8c6c0-9454-4dc6-98e8-c41cbf1c0cad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86dbe8b256d2148fe6bdc7c28429f90cf8f9e782
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383186"
---
# <a name="windows-kernel-mode-executive-support-library"></a>Windows 内核模式执行支持库


Windows 操作系统使用术语*executive 层*来指代内核模式组件，提供各种服务添加到设备驱动程序，包括：

-   对象管理

-   内存管理

-   进程和线程管理

-   输入/输出管理

-   配置管理

几个库一样，每个上述管理器提供直接的接口连接到其单独的技术。 但是，组合在一起作为 Executive 库通用接口的例程通常前缀为"**Ex**"，例如**ExGetCurrentResourceThread**。 Executive 库例程的列表，请参阅[Executive 库支持例程](https://msdn.microsoft.com/library/windows/hardware/ff544582)。

请注意 executive 层组件属于 Ntoskrnl.exe，但驱动程序和 HAL 不是管理层的层的一部分。

 

 




