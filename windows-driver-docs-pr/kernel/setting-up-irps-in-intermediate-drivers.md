---
title: 在中间驱动程序中设置 IRP
description: 在中间驱动程序中设置 IRP
ms.assetid: 0d04a951-a68e-4fa1-bdc6-dd92ec49deae
keywords:
- 可移动媒体 WDK 内核，中间驱动程序 Irp
- 中级驱动程序 Irp WDK 可移动介质
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b07e2a30bf007b1cb389368b2c7cc6741fadf69f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190446"
---
# <a name="setting-up-irps-in-intermediate-drivers"></a>在中间驱动程序中设置 IRP





在文件系统驱动程序和可移动媒体设备驱动程序之间分层的任何中间驱动程序必须在 Irp 中设置下一级驱动程序的 i/o 堆栈位置。 从传入 [**IRP \_ mj \_ 读取**](./irp-mj-read.md)、 [**irp \_ mj \_ 写入**](./irp-mj-write.md)和 [**irp \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求，中间驱动程序必须将其自己的 i/o 堆栈位置 **标志** 复制到下一个较低级别的驱动程序的 i/o 堆栈位置，同时为低级驱动程序设置 i/o 堆栈位置。

如果中间驱动程序为低级别可移动媒体驱动程序分配新的 Irp，则必须按如下所示设置这些 Irp：

-   对于传输请求，它必须在每个由驱动程序分配的 IRP 中设置线程上下文，使其与原始 IRP 中的 " **重叠** " 的值相同。

-   对于 **irp \_ mj \_ 读取**、 **irp \_ mj \_ 写入**和 **irp \_ mj \_ 设备 \_ 控制** 请求，它必须将 i/o 堆栈位置 **标志** 从原始 irp 复制到每个驱动程序分配的 irp。

否则，文件系统既不能维护缓存文件数据的完整性，也不会导致提示用户重新装载保存打开的文件的媒体。

 

