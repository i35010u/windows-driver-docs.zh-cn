---
title: 在 HwScsiFindAdapter 中设置 ConfigInfo
description: 在 HwScsiFindAdapter 中设置 ConfigInfo
ms.assetid: f9c5d23d-feab-4cc4-9cd9-29c21d4fdf0b
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- ConfigInfo
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 19e20b64c7e753031487ce3c648bdec6d93c4586
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191643"
---
# <a name="setting-up-configinfo-in-hwscsifindadapter"></a>在 HwScsiFindAdapter 中设置 ConfigInfo

对于受支持的 HBA， [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 例程可以调用 [**ScsiPortGetBusData**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetbusdata) 并检查返回的特定于总线类型的配置信息（如 POS 数据或 EISA 配置数据）。

如果输入 PORT_CONFIGURATION_INFORMATION 中的 **AccessRanges** 元素 (端口驱动程序已填充了 *ConfigInfo* 缓冲器) ，则 *HwScsiFindAdapter* 例程应将与总线相关的访问范围映射到 [**ScsiPortGetDeviceBase**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase) ，并使用返回的逻辑访问范围地址与 HBA 通信。 如果访问范围地址由端口驱动程序提供，则 *HwScsiFindAdapter* 不得在该 i/o 总线上的其他位置扫描 hba。

此外，如果端口驱动程序提供访问范围值，则 *HwScsiFindAdapter* 不得使用 *HwContext* 参数。 此类访问范围值通常附带附加的配置信息，指示即插即用的环境。 在此类环境中， *HwScsiFindAdapter* 将在微型端口驱动程序的 [**DriverEntry**](driverentry-of-scsi-miniport-driver.md) 例程返回后调用，因而 *HwContext* 指针不再有效。 仅从端口驱动程序接收无访问范围值的驱动程序，并且对受支持的 Hba 执行其自己的扫描时，可以安全地使用 *HwContext* 指针。

如果输入 [PORT_CONFIGURATION_INFORMATION](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) 包含的配置信息不是以前由 [HW_INITIALIZATION_DATA (SCSI) ](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)中的微型端口驱动程序提供的配置信息，则 *HwScsiFindAdapter* 可以使用 [**ScsiPortGetBusData**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetbusdata) 返回的值; 如果需要，则为 **AccessRanges** 元素设置微型端口驱动程序定义的默认值、 **BusInterruptLevel** 或 **BusInterruptVector**、 **DmaChannel** 或 **DmaPort** （如果 HBA 使用系统 DMA）和 **InitiatorBusId**。

在访问总线上的 HBA*之前*， *HwScsiFindAdapter*必须调用[**ScsiPortValidateRange**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportvalidaterange)来检查是否可以安全地使用此类微型端口驱动程序提供的访问范围。 如果 **ScsiPortValidateRange** 返回 **TRUE**，微型端口驱动程序可以调用 [**ScsiPortGetDeviceBase**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase) 来映射范围，并使用在调用 **ScsiPortRead * * * xxx* 和/或 **ScsiPortWrite * * xxx* 时返回的逻辑地址来确定它是否在 i/o 总线上支持 HBA。 如果 **ScsiPortValidateRange** 返回 **FALSE**，微型端口驱动程序不得尝试映射和使用这些与总线相关的访问范围值。

同样，如果端口驱动程序调用即插即用微型端口驱动程序来检测 nonenumerable 总线上的设备，则微型端口驱动程序必须在调用 **ScsiPortGetDeviceBase**之前验证访问范围。

如果端口驱动程序提供中断配置信息，微型端口驱动程序必须接受它，如果其 HBA 支持可编程中断配置，则应将其 HBA 计划为使用提供的中断值。 如果未提供任何中断配置（如值为零或值 SP_UNINITIALIZED_VALUE 所示），微型端口驱动程序应在 HBA 支持使用跳线选择时查询其 HBA，或应提供非零的默认中断配置，除非 HBA 不使用中断。 中断配置值0指示微型端口驱动程序在轮询模式下控制其 HBA。

当 *HwScsiFindAdapter* 找到它可支持的 hba 时，此例程必须在 PORT_CONFIGURATION_INFORMATION 中填写相关成员（适用于其 HBA 和给定的 **AdapterInterfaceType**）。 提供访问范围的微型端口驱动程序必须填写 **AccessRanges** 信息，将每个 **AccessRanges** 元素的总线相关 **RangeStart** 值转换为 [**ScsiPortConvertUlongToPhysicalAddress**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportconvertulongtophysicaladdress) ，然后才能为 PORT_CONFIGURATION_INFORMATION 中的范围设置总线相对基址。

对于支持的 HBA， *HwScsiFindAdapter* 还应将 **ScsiPortGetDeviceBase** 返回的映射逻辑范围地址保存在微型端口驱动程序的设备扩展中。 每个微型端口驱动程序必须调用具有这些映射的系统)  (地址的 **ScsiPortRead * * * xxx*和 **ScsiPortWrite * **

对于 i/o 空间中每个成功验证和映射的范围，微型端口驱动程序调用 **ScsiPortRead/WritePort * * Xxx* 例程与其 HBA 通信。 对于内存空间中的每个此类范围，微型端口驱动程序将调用 **ScsiPortRead/WriteRegister * * * Xxx*。

对于 "兼容" HBA， *HwScsiFindAdapter* 应检查输入 **Atdisk。已声明** 成员，并尝试通过将该值重置为 **TRUE**来声明 "AT" 范围。