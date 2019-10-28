---
title: 存储类驱动程序简介
description: 存储类驱动程序简介
ms.assetid: 0ea462a9-5e6f-419f-af36-50f50901143d
keywords:
- 存储类驱动程序 WDK，关于存储类驱动程序
- 类驱动程序 WDK 存储，关于存储类驱动程序
- HBA WDK 存储
ms.date: 10/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 94049848af080157b95f778f6eb7190f7a56cca2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838092"
---
# <a name="introduction-to-storage-class-drivers"></a>存储类驱动程序简介

## <span id="ddk_introduction_to_storage_class_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_STORAGE_CLASS_DRIVERS_KG"></span>

*存储类驱动程序*使用已建立良好的 SCSI 类/端口接口，在系统提供存储端口驱动程序（当前为 SCSI、IDE、USB 和 IEEE 1394）的任何总线上控制其类型的大容量存储设备。 存储设备连接到的特定总线对于存储类驱动程序是透明的。

任何存储类驱动程序都通过构建包含*命令描述符块*（CDBs）的*SCSI 请求块*（SRBs），并通过任何干预筛选器驱动程序（通过任何干预筛选器驱动程序）将这些请求发送到基础存储端口驱动程序。

存储类驱动程序在 SRB 中不提供寻址信息。 相反，端口驱动程序（或静止的驱动程序）负责任何所需的寻址。 存储端口驱动程序将 SRBs 转换为底层主机总线适配器（HBA）所需的格式，该格式可能是 SCSI 或1394主机总线适配器、IDE 控制器或其他此类硬件，并向设备发出命令。 在 Windows 驱动程序工具包（WDK）中，术语 "HBA" 代表任何此类基础适配器或控制器。

对于在存储类驱动程序上分层的 i/o 管理器和任何更高级别的驱动程序，大多数存储类驱动程序都是标准的内核模式中间驱动程序。 因此，每个类驱动程序必须有一个[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程、一个[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程、一个[**卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程、一个或多个[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程、 [**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来处理插件和播放和电源 Irp。

存储类驱动程序还必须具有[**DispatchSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来处理系统控制 irp，并可具有任何其他标准级别的驱动程序例程（如[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，如驱动程序设计器所确定的那样）。 有关系统控制和标准内核模式驱动程序例程的详细信息，请参阅[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

对于 PnP 管理器，存储类驱动程序是一种[功能驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)，即驱动单个设备的驱动程序。 存储类驱动程序还可以充当[总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)，枚举其设备的子设备。 例如，分区媒体设备（如磁盘）的类驱动程序会返回表示其分区的 PDOs 的列表。 每个此类 PDO 都可以作为目标设备进行寻址，并由其自己的类驱动程序提供服务。

**请注意**   应按照本部分中所述来实现 SCSI 设备（如打印机）的驱动程序或扫描仪。 此类 SCSI 设备的驱动程序利用相同的 SCSI 类/端口接口控制其设备，并具有相同的责任来处理 Irp，生成 SRBs，并将其作为存储设备的驱动程序发送到基础端口驱动程序。
