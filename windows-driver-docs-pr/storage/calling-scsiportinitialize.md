---
title: 调用 ScsiPortInitialize
description: 调用 ScsiPortInitialize
ms.assetid: a736f279-9ade-4043-90f7-209fca260a39
keywords:
- ScsiPortInitialize
- 初始化 SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa8f7c1009ad963789f8d421e07544e6f331ab33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368366"
---
# <a name="calling-scsiportinitialize"></a>调用 ScsiPortInitialize


## <span id="ddk_calling_scsiportinitialize_kg"></span><span id="DDK_CALLING_SCSIPORTINITIALIZE_KG"></span>


如果可以连接在多个类型的 I/O 总线上的微型端口驱动程序的 HBA，微型端口驱动程序必须调用[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)每个总线类型和可以具有不同*HwScsiFindAdapter*例程的每个总线类型。

每次调用后**ScsiPortInitialize**，这样的微型端口驱动程序必须：

-   修改 AdapterInterfaceType 成员。

-   修改在 HwScsiFindAdapter 成员[ **HW\_初始化\_数据 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)微型端口驱动程序是否该总线类型的不同 HwScsiFindAdapter 例程。

-   修改新的总线类型的微型端口驱动程序提供的上下文数据。

-   为每种类型的可能在其连接支持的 HBA 的总线调用 ScsiPortInitialize。

如果微型端口驱动程序是一个旧驱动程序不支持插**ScsiPortInitialize**调用微型端口驱动程序*HwScsiFindAdapter*例程一个或多个时间才会返回到控件微型端口驱动程序[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)例程。 所有[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))微型端口驱动程序的上下文中调用**DriverEntry**例程，按顺序**DriverEntry**称为**ScsiPortInitialize**。

如果微型端口驱动程序支持插**ScsiPortInitialize**存储初始化数据以供将来使用，并返回状态\_微型端口驱动程序的成功**DriverEntry**例程。 端口驱动程序不会调用微型端口驱动程序*HwScsiFindAdapter*例程直到插管理器检测到为其微型端口驱动程序注册为服务的 HBA。

端口驱动程序对于插和旧的微型端口驱动程序，执行以下所有调用微型端口驱动程序之前*HwScsiFindAdapter*例程：

-   检查硬件的有效性\_初始化\_数据。

-   收集并存储在其创建表示 HBA 的设备对象的设备扩展中的相关信息。

-   分配的内存，并使用零初始化设备微型端口驱动程序可以在其中存储有关 HBA 驱动程序确定信息所请求大小的扩展。

-   分配的配置信息缓冲区，则内存**sizeof**([**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information))。

-   在配置信息缓冲区，将填充为在端口中\_配置\_有关 HBA 上特定 I/O 尽可能配置信息的信息结构总线从微型端口驱动程序提供 HW尽可能\_初始化\_数据和从其他源，例如旧的微型端口驱动程序的注册表或插微型端口驱动程序的插管理器。

有关微型端口驱动程序的详细信息*HwScsiFindAdapter*例程，请参阅[SCSI 微型端口驱动程序 HwScsiFindAdapter 例程](scsi-miniport-driver-s-hwscsifindadapter-routine.md)。

如果微型端口驱动程序**DriverEntry**例程设置特定**AdapterInterfaceType**的 HW 中的值\_初始化\_但没有数据是中该类型没有总线计算机，端口驱动程序返回特定于操作系统的状态值，该值指示此类 HBA 不存在当前计算机中。 它不会调用驱动程序提供*HwScsiFindAdapter*例程该总线类型。

微型端口驱动程序不会保持已加载，如果计算机上存在指定的微型端口驱动程序的类型没有 I/O 总线**DriverEntry**例程。

旧的微型端口驱动程序，请注意**ScsiPortInitialize**还负责以下控件返回到旧的微型端口驱动程序之前**DriverEntry**例程：

-   设置所有必要的系统对象。

-   获取在注册表中的配置信息和设置配置信息。

-   代表微型端口驱动程序分配系统资源，包括内存在的金额中指示的微型端口驱动程序指定**DeviceExtensionSize**， **SpecificLuExtensionSize**，和/或**SrbExtensionSize**在微型端口驱动程序可以维护特定于 HBA 的状态、 逻辑单元状态和/或每个请求的状态，分别。

插微型端口驱动程序的端口驱动程序执行这些操作后微型端口驱动程序*HwScsiFindAdapter*例程的返回和端口驱动程序调用微型端口驱动程序之前[ *HwScsiInitialize* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))例程。

每个 SCSI 微型端口驱动程序定义的内部结构和其设备扩展、 逻辑单元扩展 （如果有） 和 SRB 扩展 （如果有） 的内容。 指向特定于 HBA 的设备扩展的是除每个系统定义的微型端口驱动程序例程的输入的参数**DriverEntry**。 许多 **ScsiPort * * * Xxx*例程需要此指针作为参数。

**ScsiPortInitialize**只能从微型端口驱动程序可以调用**DriverEntry**例程。 有关详细信息，请参阅[ **HW\_初始化\_数据 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)并[ **ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)。

 

 




