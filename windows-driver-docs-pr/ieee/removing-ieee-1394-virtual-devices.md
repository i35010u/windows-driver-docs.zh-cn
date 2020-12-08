---
title: 删除 IEEE 1394 虚拟设备
description: 删除 IEEE 1394 虚拟设备
keywords:
- 模拟驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- 虚拟设备 WDK IEEE 1394 总线
- 删除虚拟设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42c9dd5990ccea3bf16232ad3d61330846cacd6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819575"
---
# <a name="removing-ieee-1394-virtual-devices"></a>删除 IEEE 1394 虚拟设备





可通过两种方法 (PDO) 虚拟设备中删除物理设备对象：

1.  **标准即插即用 (PnP) 删除设备的方法**。 若要使用此方法，请让你的驱动程序将 [**IRP \_ MN \_ REMOVE \_ 设备**](../kernel/irp-mn-remove-device.md) 请求发送到虚拟设备。

    I/o 堆栈应包含以下值：

    -   **MajorFunction** = IRP \_ MJ \_ PNP
    -   **MinorFunction** = IRP \_ MN \_ 删除 \_ 设备

2.  **I/o 请求数据包 (IRP) 类型** IOCTL \_ IEEE1394 \_ API \_ 请求：若要使用此方法，请让你的驱动程序将 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 请求发送到虚拟设备。

    I/o 堆栈应包含以下值：

    -   **MajorFunction** = IRP \_ MJ \_ 设备 \_ 控制
    -   **DeviceIoControl. IoControlCode**  = [ **IOCTL \_ IEEE1394 \_ API \_ 请求**](https://msdn.microsoft.com/library/windows/hardware/ff537241)

    IRP 应包含以下值：

    -   **AssocicatedIrp.SystemBuffer- &gt;SystemBuffer** 指向 [**IEEE1394 \_ API \_ 请求**](/previous-versions/ff537204(v=vs.85)) 结构
    -   IEEE1394 api 请求的 **RequestNumber** 成员 \_ \_ = [ **IEEE1394 \_ api \_ 删除 \_ 虚拟 \_ 设备**](https://msdn.microsoft.com/library/windows/hardware/ff537201)

第一种方法 (IRP \_ MN \_ remove \_ device) 将删除该设备，但如果该设备是永久性的，则下次计算机启动时，它将被还原。 第二种方法 (IEEE1394 \_ API \_ 删除 \_ 虚拟 \_ 设备) 完全删除该设备，以便在重新启动后，它将不再存在。 下次计算机启动时，将不会还原设备。

请注意，上层驱动程序或用户模式服务可以通过常用的 PnP 机制确定哪些虚拟设备存在。 此机制使用虚拟驱动程序的 INF 文件中提供的类 GUID。

 

