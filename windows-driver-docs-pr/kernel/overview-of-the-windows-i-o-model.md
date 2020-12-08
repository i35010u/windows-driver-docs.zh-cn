---
title: Windows I/O 模型概述
description: Windows I/O 模型概述
keywords:
- Irp WDK 内核，关于 Windows i/o 模型
- Windows i/o 模型 WDK
- I/o WDK 内核，模型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049cf084bd2f1bc67cfa3483f37500c8f70b8157
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803541"
---
# <a name="overview-of-the-windows-io-model"></a>Windows I/O 模型概述





每个操作系统都具有隐式或显式 i/o 模型，可用于处理发件和外围设备的数据流。 Microsoft Windows i/o 模型的一项功能是它对异步 i/o 的支持。 此外，i/o 模型具有以下常规功能：

-   I/o 管理器为所有内核模式驱动程序提供了一个一致的接口，包括最低级别、中间和文件系统驱动程序。 驱动程序的所有 i/o 请求都作为 i/o 请求数据包发送 (Irp) 。

-   I/o 操作是分层的。 I/o 管理器将导出 i/o 系统服务，这些服务受保护的子系统将调用，代表其应用程序和/或最终用户执行 i/o 操作。 I/o 管理器会截获这些调用，设置一个或多个 Irp，并通过可能的分层驱动程序将其路由到物理设备。

-   I/o 管理器定义了驱动程序可以支持的一组标准例程，一些必需和其他选项是可选的。 所有驱动程序都遵循相对一致的实现模型，因为外围设备与总线、函数、筛选器和文件系统驱动程序所需的功能不同。

-   与操作系统本身一样，驱动程序基于对象。 驱动程序、其设备和系统硬件表示为对象。 I/o 管理器和其他操作系统组件导出内核模式支持例程，驱动程序可调用这些例程来通过操作适当的对象来完成工作。

除了使用 Irp 传递传统 i/o 请求以外，i/o 管理器还与 PnP 和电源管理器一起使用，发送包含 PnP 和电源请求的 Irp。

 

 




