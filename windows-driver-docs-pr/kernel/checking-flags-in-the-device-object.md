---
title: 检查设备对象中的标志
description: 检查设备对象中的标志
keywords:
- 可移动媒体 WDK 内核，标志检查
- 标志 WDK 可移动介质
- 检查设备对象标志
- 验证设备对象标志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 385ce3cbae5a994d249e88e613152fa1487091c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825659"
---
# <a name="checking-flags-in-the-device-object"></a>检查设备对象中的标志





对于从可移动媒体请求 i/o 操作的每个 IRP，可移动媒体设备驱动程序必须确定是否 \_ \_ 已在其 **DeviceObject &gt; 标记** 中设置了 "验证卷"。 如果设置了此值，则驱动程序必须执行以下操作：

-   对于 [**irp \_ mj \_ 读取**](./irp-mj-read.md)、 [**irp \_ mj \_ 写入**](./irp-mj-write.md)和 [**irp \_ Mj \_ 设备 \_ 控制**](./irp-mj-device-control.md)请求，请 \_ \_ \_ 在驱动程序的 [**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的 **Flags** 成员中检查是否设置了 SL 替代验证卷。 如果是，则继续执行请求的操作。

    当 IFS 装入或逐可移动介质卷时，返回有关基础媒体逻辑结构的信息的设备控制请求具有 SL \_ 替代 \_ 验证 \_ 在 I/o 堆栈位置 **标志** 成员中设置的卷。

-   否则，驱动程序必须拒绝为相应的驱动器、设备或分区执行 i/o 请求，同时 \_ 验证 \_ 卷是否设置为其 **DeviceObject &gt; 标志**。 可移动媒体驱动程序必须将 Irp 发送到相应的设备，如前一节所述，为每个 IRP 重复步骤3和4，直到 FSD 清除 \_ \_ 了可移动媒体驱动程序的 **DeviceObject &gt;** 中的 "验证" 卷。

如果在设置 "验证卷" 时，可移动媒体设备驱动程序不会失败， \_ \_ 并且 \_ \_ \_ 没有为上述传输请求设置 SL 替代验证卷，则文件系统既不能维护缓存的文件数据的完整性，也不会导致提示用户重新装载保存打开的文件的媒体。

 

