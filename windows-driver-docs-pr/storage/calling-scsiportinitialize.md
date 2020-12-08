---
title: 调用 ScsiPortInitialize
description: 调用 ScsiPortInitialize
keywords:
- ScsiPortInitialize
- 初始化 SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2803bc12649ba5dd87d1b58e136af02cd5f253ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804753"
---
# <a name="calling-scsiportinitialize"></a>调用 ScsiPortInitialize


## <span id="ddk_calling_scsiportinitialize_kg"></span><span id="DDK_CALLING_SCSIPORTINITIALIZE_KG"></span>


如果可将微型端口驱动程序的 HBA 连接到多种类型的 i/o 总线，微型端口驱动程序必须为每个总线类型调用 [**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize) ，并为每个总线类型使用不同的 *HwScsiFindAdapter* 例程。

每次调用 **ScsiPortInitialize** 后，此类微型端口驱动程序必须：

-   修改 AdapterInterfaceType 成员。

-   如果微型端口驱动程序为该总线类型使用了不同的 HwScsiFindAdapter 例程，请在 HwScsiFindAdapter 中修改 [**HW \_ 初始化 \_)  (数据**](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data) 中的成员。

-   修改小型端口驱动程序提供的新总线类型上下文数据。

-   为每种类型的总线（可在其上连接支持的 HBA）调用 ScsiPortInitialize。

如果微型端口驱动程序是不支持即插即用的旧驱动程序，则 **ScsiPortInitialize** 会在将控制返回给微型端口驱动程序的 [**DriverEntry**](scsi-miniport-driver-s-driverentry-routine.md)例程之前，先调用微型端口驱动程序的 *HwScsiFindAdapter* 例程一次或多次。 所有 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 调用都在微型端口驱动程序的 **DriverEntry** 例程的上下文中进行，并按顺序 **DriverEntry** 调用 **ScsiPortInitialize**。

如果微型端口驱动程序支持即插即用，则 **ScsiPortInitialize** 存储初始化数据以供将来使用，并将状态 \_ 成功返回给微型端口驱动程序的 **DriverEntry** 例程。 端口驱动程序不会调用微型端口驱动程序的 *HwScsiFindAdapter* 例程，直到即插即用 manager 检测到一个 HBA，其中微型端口驱动程序已注册为服务。

对于即插即用和旧微型端口驱动程序，端口驱动程序会在调用微型端口驱动程序的 *HwScsiFindAdapter* 例程之前执行以下所有操作：

-   检查 HW 初始化数据的有效性 \_ \_ 。

-   收集并存储其创建的设备对象的设备扩展中的相关信息，以代表 HBA。

-   为分配内存并将其初始化为零：请求的大小的设备扩展，微型端口驱动程序可以存储有关 HBA 的驱动程序确定信息。

-   **为 (** [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)) 的配置信息缓冲区分配内存。

-   在配置信息缓冲区中，会尽可能 \_ \_ 多地在特定 i/o 总线上的 HBA 中填充端口配置信息结构，从微型端口驱动程序提供的 HW \_ 初始化 \_ 数据和其他源（例如用于旧微型端口驱动程序的注册表或即插即用微型端口驱动程序的即插即用管理器）。

有关微型端口驱动程序的 *HwScsiFindAdapter* 例程的详细信息，请参阅 [SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程](scsi-miniport-driver-s-hwscsifindadapter-routine.md)。

如果微型端口驱动程序的 **DriverEntry** 例程在 HW 初始化数据中设置特定的 **AdapterInterfaceType** 值 \_ \_ ，但计算机中不存在该类型的总线，则端口驱动程序将返回特定于操作系统的状态值，指出此类 HBA 在当前计算机中不存在。 它不会为该总线类型调用驱动程序提供的 *HwScsiFindAdapter* 例程。

如果计算机没有 (s 类型的 i/o 总线（) 微型端口驱动程序的 **DriverEntry** 例程指定），则不会保持加载微型端口驱动程序。

对于旧版微型端口驱动程序，请注意， **ScsiPortInitialize** 在将控制返回到旧版微型端口驱动程序的 **DriverEntry** 例程之前，还负责执行以下操作：

-   设置所有必需的系统对象。

-   从获取配置信息并在注册表中设置配置信息。

-   代表微型端口驱动程序分配系统资源（包括由微型端口驱动程序指定的 **DeviceExtensionSize**、 **SpecificLuExtensionSize** 和/或 **SrbExtensionSize** 所指示的数量中的内存），其中，微型端口驱动程序可分别维护特定于 HBA 的状态、每个逻辑单元的状态和/或每个请求状态。

对于即插即用微型端口驱动程序，端口驱动程序会在微型端口驱动程序的 *HwScsiFindAdapter* 例程返回之后、端口驱动程序调用微型端口驱动程序的 [*HwScsiInitialize*](/previous-versions/windows/hardware/drivers/ff557302(v=vs.85)) 例程之后执行这些操作。

每个 SCSI 微型端口驱动程序定义其设备扩展的内部结构和内容、逻辑单元扩展 (如果任何) ，以及任何)  (的 SRB 扩展。 指向特定于 HBA 的设备扩展的指针是每个系统定义的微型端口驱动程序例程（ **DriverEntry** 除外）的输入参数。 许多 **ScsiPort**_Xxx_ 例程需要此指针作为参数。

只能从微型端口驱动程序的 **DriverEntry** 例程调用 **ScsiPortInitialize** 。 有关详细信息，请参阅 [**HW \_ 初始化 \_ 数据 (SCSI)**](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data) 和 [**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)。

 

