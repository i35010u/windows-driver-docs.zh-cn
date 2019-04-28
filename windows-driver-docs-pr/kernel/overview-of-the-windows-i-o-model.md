---
title: Windows I/O 模型概述
description: Windows I/O 模型概述
ms.assetid: 17a012b7-946e-4f42-8d80-e270bc26de06
keywords:
- Irp WDK 内核，有关 Windows I/O 模型
- Windows I/O 模型 WDK
- I/O WDK 内核、 模型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b86daddcaf0016aa417d5cf54ce6db32f57f79d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352065"
---
# <a name="overview-of-the-windows-io-model"></a>Windows I/O 模型概述





每个操作系统提供了用于处理数据流与外围设备之间的隐式或显式 I/O 模式。 Microsoft Windows I/O 模型的一个功能是它支持异步 I/O。 此外，I/O 模型具有以下常规功能：

-   I/O 管理器提供所有内核模式驱动程序的一致界面，包括最低级别，中间，和文件系统驱动程序。 I/O 请求数据包 (Irp) 作为发送到驱动程序的所有 I/O 请求。

-   I/O 操作的分层。 I/O 管理器将导出 I/O 系统服务，哪些用户模式下受保护的子系统调用执行 I/O 操作代表其应用程序和/或最终用户。 I/O 管理器截获这些调用，设置一个或多个 Irp，并将其路由到物理设备可能是分层驱动程序通过。

-   I/O 管理器定义一组标准的例程、 某些必需和可选的驱动程序可以支持其他人。 所有驱动程序都遵循一个相对统一实施模型，提供在外围设备和所需的总线、 函数、 筛选和文件系统驱动程序的不同功能之间的差异。

-   与操作系统本身，驱动程序是基于对象的。 驱动程序、 其设备和系统硬件表示为对象。 I/O 管理器和其他操作系统组件导出驱动程序可以调用的操作相应的对象完成工作的内核模式下支持例程。

除了使用 Irp 传达传统的 I/O 请求，I/O 管理器配合 PnP 和电源管理器发送 Irp 包含 PnP 和电源的请求。

 

 




