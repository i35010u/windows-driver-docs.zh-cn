---
title: 在 HwScsiFindAdapter 中设置 ConfigInfo
description: 在 HwScsiFindAdapter 中设置 ConfigInfo
ms.assetid: f9c5d23d-feab-4cc4-9cd9-29c21d4fdf0b
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
- ConfigInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79202cefaac4ad7108ab81cf057d96e661b761b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341218"
---
# <a name="setting-up-configinfo-in-hwscsifindadapter"></a>在 HwScsiFindAdapter 中设置 ConfigInfo


## <span id="ddk_setting_up_configinfo_in_hwscsifindadapter_kg"></span><span id="DDK_SETTING_UP_CONFIGINFO_IN_HWSCSIFINDADAPTER_KG"></span>


[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)例程可以调用[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)并检查返回的总线类型特定配置信息，例如 POS 数据或 EISA 配置数据，受支持的 HBA。

如果**AccessRanges**输入端口中的元素\_配置\_信息 ( *ConfigInfo*缓冲区) 端口驱动程序，通过填写*HwScsiFindAdapter*例程应映射使用的总线相对访问范围[ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629) ，并使用到的地址返回的逻辑访问范围HBA 与进行通信。 如果端口驱动程序，提供了访问的地址范围*HwScsiFindAdapter*必须扫描该 I/O 总线上的其他位置的 Hba。

此外，如果端口驱动程序提供访问范围的值， *HwScsiFindAdapter*不能使用*HwContext*参数。 此类访问范围值通常伴随指示插环境的其他配置信息。 在此类环境中， *HwScsiFindAdapter*微型端口驱动程序后调用[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)例程返回，因此*HwContext*指针将不再有效。 可以安全地使用唯一的驱动程序的接收端口驱动程序从零访问范围值然后，执行受支持的 Hba 自己扫描*HwContext*指针。

如果输入[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)不包含配置信息以外，以前由中的微型端口驱动程序提供[ **HW\_初始化\_数据 (SCSI)**](https://msdn.microsoft.com/library/windows/hardware/ff557456)， *HwScsiFindAdapter*可以使用返回值[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)或者，如果有必要，请将微型端口驱动程序定义的默认值为**AccessRanges**元素**BusInterruptLevel**或**BusInterruptVector**， **DmaChannel**或**DmaPort**如果 HBA 使用系统 DMA，和**InitiatorBusId**。

*HwScsiFindAdapter*必须调用[ **ScsiPortValidateRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564761)若要检查是否可以安全地使用这种微型端口驱动程序提供访问范围*之前*它将访问总线上的 HBA。 如果**ScsiPortValidateRange**返回**TRUE**，微型端口驱动程序可以调用[ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)要映射的范围，并使用返回对的调用中的逻辑地址 **ScsiPortRead * * * Xxx*和/或 **ScsiPortWrite * * * Xxx*以确定它在 I/O 总线上是否都支持 HBA。 如果**ScsiPortValidateRange**返回**FALSE**，微型端口驱动程序必须尝试映射，并使用这些总线相对访问范围值。

同样，如果端口驱动程序调用插微型端口驱动程序，以检测 nonenumerable 总线上的设备，微型端口驱动程序必须验证之前调用的访问权限范围**ScsiPortGetDeviceBase**。

如果端口驱动程序提供了中断的配置信息，微型端口驱动程序必须接受它并且，如果其 HBA 支持可编程中断配置应设定其 HBA 使用提供的中断值。 如果提供无中断配置，如所示通过值为零或值 SP\_未初始化\_值，该值，微型端口驱动程序应要么查询其 HBA，如果 HBA 支持中断选择使用跳线或它应提供非零值的默认中断配置中，除非 HBA 不使用中断。 中断配置值零指示微型端口驱动程序控制其在轮询模式下的 HBA。

当*HwScsiFindAdapter*可以支持网络发现查找的 HBA，此例程必须填写相关的成员，根据其 HBA 和给定**AdapterInterfaceType**，在端口\_配置\_信息。 提供访问范围的微型端口驱动程序必须填写**AccessRanges**信息，将每个转换**AccessRanges**元素的总线相对**RangeStart**值与[ **ScsiPortConvertUlongToPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff564613)之前在该端口设置范围的总线相对基址\_配置\_信息。

对于受支持的 HBA， *HwScsiFindAdapter*还应保存返回的映射的逻辑范围地址**ScsiPortGetDeviceBase**微型端口驱动程序的设备扩展中。 每个微型端口驱动程序必须调用 **ScsiPortRead * * * Xxx*和 **ScsiPortWrite * * * Xxx*使用这些映射系统地址，其 HBA(s) 与进行通信。

对于每个已成功验证和映射在 I/O 空间中的范围，微型端口驱动程序调用 **ScsiPortRead/WritePort * * * Xxx*例程与其 HBA 进行通信。 对于内存空间中每个此类范围，微型端口驱动程序调用 **ScsiPortRead/WriteRegister * * * Xxx*。

为"AT 兼容"HBA *HwScsiFindAdapter*应检查输入**Atdisk...索取**成员并尝试声明一个"AT"范围通过重置为值**TRUE**。

 

 




