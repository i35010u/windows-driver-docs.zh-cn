---
title: 存储类驱动程序简介
description: 存储类驱动程序简介
ms.assetid: 0ea462a9-5e6f-419f-af36-50f50901143d
keywords:
- 存储类驱动程序 WDK，有关存储类驱动程序
- 类驱动程序 WDK 存储有关存储类驱动程序
- HBA WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10cce3a7243996a0e11b82202b1e68e0e7672e9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382113"
---
# <a name="introduction-to-storage-class-drivers"></a>存储类驱动程序简介


## <span id="ddk_introduction_to_storage_class_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_STORAGE_CLASS_DRIVERS_KG"></span>


一个*存储类驱动程序*使用获得广泛认可的 SCSI 类/端口接口来控制其类型，则系统将为其提供存储端口驱动程序 （当前 SCSI、 IDE、 USB 和 IEEE 1394） 任何总线上的大容量存储设备。 存储设备连接到特定的总线是透明的存储类驱动程序。

任何存储类驱动程序处理来自用户的应用程序或更高级别的驱动程序的 I/O 请求通过构建*SCSI 请求块*(Srb) 包含*命令描述符块*(Cdb) 和发送它们，通过任何干预筛选器驱动程序，到基础存储端口驱动程序。

存储类驱动程序不提供 SRB 中的寻址信息。 相反，端口驱动程序 （或仍较低的驱动程序） 是负责所需任何寻址。 存储端口驱动程序将 Srb 转换所需的基础主机总线适配器 (HBA)，这可能是 SCSI 或 1394年主机总线适配器、 IDE 控制器或其他此类硬件的格式为，并向设备发出命令。 在 Windows Driver Kit (WDK) 中，术语"HBA"代表任何此类基础适配器或控制器。

I/O 管理器和分层存储类驱动程序的任何更高级别的驱动程序，大多数存储类驱动程序是标准的内核模式中间驱动程序。 因此，每个类驱动程序必须具有[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程， [ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程，一个或多个[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，加上[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程来处理插和 power Irp。

存储类驱动程序还必须具有[ **DispatchSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程来处理系统控制 Irp，并且能与任何其他标准更高级别的驱动程序例程，如[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，由驱动程序设计器。 有关系统控制和标准的内核模式驱动程序例程的详细信息，请参阅[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

存储类驱动程序是即插即用管理器中，向[功能的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff546516)，即，一个驱动器单个设备。 存储类驱动程序也可用作[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)，枚举子其设备的设备。 例如，如磁盘分区的媒体设备的类驱动程序返回一系列 PDOs 表示其分区。 每个此类 PDO 可以用作目标设备，并且由其自己的类驱动程序提供服务。

**请注意**  应实现的 SCSI 设备，如打印机或扫描仪的驱动程序，如本部分中所述。 这样的 SCSI 设备的驱动程序使用相同的 SCSI 类/端口接口来控制其设备，并且具有相同的职责来处理 Irp，生成 Srb，并将其发送到基础端口驱动程序存储设备的驱动程序也一样。

 

 

 




