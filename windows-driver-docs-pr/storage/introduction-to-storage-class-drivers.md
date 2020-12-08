---
title: 存储类驱动程序简介
description: 存储类驱动程序简介
keywords:
- 存储类驱动程序 WDK，关于存储类驱动程序
- 类驱动程序 WDK 存储，关于存储类驱动程序
- HBA WDK 存储
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8e74a2f8745edbd5315893ac59b6ac1eef6d8d6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811693"
---
# <a name="introduction-to-storage-class-drivers"></a>存储类驱动程序简介

*存储类驱动程序* 使用已建立良好的 SCSI 类/端口接口控制其类型的大容量存储设备，该设备在系统提供存储端口驱动程序 (当前 SCSI、IDE、USB 和 IEEE 1394) 的任何总线上。 存储设备连接到的特定总线对于存储类驱动程序是透明的。

任何存储类驱动程序都通过构建 *SCSI 请求块* 来处理来自用户应用程序或更高级别的驱动程序的 i/o 请求， (SRBs) 包含 *命令描述符块* (CDBs) ，并通过任何干预筛选器驱动程序将这些块发送到基础存储端口驱动程序。

存储类驱动程序在 SRB 中不提供寻址信息。 相反，端口驱动程序 (或静止的驱动程序) 负责任何所需的寻址。 存储端口驱动程序将 SRBs 转换为底层主机总线适配器所需的格式 (HBA) ，可能是 SCSI 或1394主机总线适配器、IDE 控制器或其他此类硬件，并向设备发出命令。 在 Windows 驱动程序工具包 (WDK) 中，术语 "HBA" 代表任何此类基础适配器或控制器。

对于在存储类驱动程序上分层的 i/o 管理器和任何更高级别的驱动程序，大多数存储类驱动程序都是标准的内核模式中间驱动程序。 因此，每个类驱动程序必须具有 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程、 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程、 [**卸载**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程、一个或多个 [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程以及用于处理即插即用和电源 irp 的 [**DispatchPnP**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [**DispatchPower**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程。

存储类驱动程序还必须具有 [**DispatchSystemControl**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程来处理系统控制 irp，并可具有任何其他标准级别的驱动程序例程（如 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，如驱动程序设计器所确定的那样）。 有关系统控制和标准内核模式驱动程序例程的详细信息，请参阅 [标准驱动程序例程](../kernel/introduction-to-standard-driver-routines.md)。

对于 PnP 管理器，存储类驱动程序是一种 [功能驱动程序](../kernel/function-drivers.md)，即驱动单个设备的驱动程序。 存储类驱动程序还可以充当 [总线驱动程序](../kernel/bus-drivers.md)，枚举其设备的子设备。 例如，分区媒体设备（如磁盘）的类驱动程序会返回表示其分区的 PDOs 的列表。 每个此类 PDO 都可以作为目标设备进行寻址，并由其自己的类驱动程序提供服务。

> [!NOTE]
> 如本部分中所述，应实现 SCSI 设备（如打印机）的驱动程序或扫描仪。 此类 SCSI 设备的驱动程序利用相同的 SCSI 类/端口接口控制其设备，并具有相同的责任来处理 Irp，生成 SRBs，并将其作为存储设备的驱动程序发送到基础端口驱动程序。
