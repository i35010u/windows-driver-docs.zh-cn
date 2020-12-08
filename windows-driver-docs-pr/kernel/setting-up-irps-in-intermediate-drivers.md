---
title: 在中间驱动程序中设置 IRP
description: 在中间驱动程序中设置 IRP
keywords:
- 可移动媒体 WDK 内核，中间驱动程序 Irp
- 中级驱动程序 Irp WDK 可移动介质
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e6c2e273c8bc6cd0c2548bf5f8360e18fcb3cee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837971"
---
# <a name="setting-up-irps-in-intermediate-drivers"></a>在中间驱动程序中设置 IRP





在文件系统驱动程序和可移动媒体设备驱动程序之间分层的任何中间驱动程序必须在 Irp 中设置下一级驱动程序的 i/o 堆栈位置。 从传入 [**IRP \_ mj \_ 读取**](./irp-mj-read.md)、 [**irp \_ mj \_ 写入**](./irp-mj-write.md)和 [**irp \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求，中间驱动程序必须将其自己的 i/o 堆栈位置 **标志** 复制到下一个较低级别的驱动程序的 i/o 堆栈位置，同时为低级驱动程序设置 i/o 堆栈位置。

如果中间驱动程序为低级别可移动媒体驱动程序分配新的 Irp，则必须按如下所示设置这些 Irp：

-   对于传输请求，它必须在每个由驱动程序分配的 IRP 中设置线程上下文，使其与原始 IRP 中的 " **重叠** " 的值相同。

-   对于 **irp \_ mj \_ 读取**、 **irp \_ mj \_ 写入** 和 **irp \_ mj \_ 设备 \_ 控制** 请求，它必须将 i/o 堆栈位置 **标志** 从原始 irp 复制到每个驱动程序分配的 irp。

否则，文件系统既不能维护缓存文件数据的完整性，也不会导致提示用户重新装载保存打开的文件的媒体。

 

