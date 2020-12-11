---
title: 使用磁带类驱动程序
description: 使用磁带类驱动程序
keywords:
- 磁带驱动程序 WDK 存储，关于磁带驱动程序
- 存储磁带驱动程序 WDK，关于磁带驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e9feedc41e5da9b0cf1fd309917e0f595ec278d
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090746"
---
# <a name="using-the-tape-class-driver"></a>使用磁带类驱动程序


## <span id="ddk_using_the_tape_class_driver_kg"></span><span id="DDK_USING_THE_TAPE_CLASS_DRIVER_KG"></span>


系统提供的磁带类驱动程序实现与设备无关的、特定于操作系统的磁带支持，并为特定于设备的磁带 miniclass 驱动程序导出支持例程。

磁带类驱动程序：

-   使用 miniclass 驱动程序的 **DriverEntry** 例程提供的特定于设备的信息来初始化磁带 miniclass 驱动程序，包括分配和初始化 miniclass 驱动程序及其支持的设备的操作系统资源，创建设备对象 (FDO) 来表示设备并将设备连接到设备堆栈，并在从 PnP 管理器收到启动请求时启动设备。

-   导出内存分配和初始化例程。

-   根据需要拆分传输请求以容纳 HBA 的最大传输大小。

-   处理 IRP \_ mj \_ CREATE、irp \_ mj \_ READ、IRP \_ mj \_ WRITE、irp \_ mj \_ PNP 和 IRP \_ mj \_ 电源请求。

-   对 IRP \_ MJ 设备控制请求执行与设备无关的预处理 \_ \_ ，并将调度发送到磁带 miniclass 驱动程序中相应的特定于设备的例程。

-   分配 SRBs 并将其发送到基础存储端口驱动程序，之后磁带 miniclass 驱动程序已填充了 CDB 以及任何其他适用于该请求的 SRB 成员。

-   在 Windows NT 状态代码和磁带状态代码之间进行转换，提供与设备无关的特定于磁带的错误处理，并调用磁带 miniclass 驱动程序的特定于设备的错误处理例程。

-   分配磁带 miniclass 驱动程序的驱动程序上下文区域 (minitape 扩展和命令扩展) 。

有关可由磁带 miniclass 驱动程序调用的 **TapeClass**_Xxx_ 例程的说明，请参阅 [磁带类驱动程序例程](/windows-hardware/drivers/ddi/minitape)。

 

