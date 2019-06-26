---
title: 设置 AdapterControl 例程
description: 设置 AdapterControl 例程
ms.assetid: 0d2add25-711a-4e5d-8409-b7ce60b08858
keywords:
- AdapterControl 例程设置
- AdapterControl 例程编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c992d6f2088e3f63faa1cc949e35eaaaa3c84c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360261"
---
# <a name="setting-up-adaptercontrol-routines"></a>设置 AdapterControl 例程





有关即插即用驱动程序的调度例程[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求必须执行以下操作[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)例程：

1.  设置设备的 DMA 功能的适配器对象通过填写[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)结构和调用[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter).

2.  保存适配器的对象指针和*NumberOfMapRegisters*返回的**IoGetDmaAdapter**。

    特定于平台的最大*NumberOfMapRegisters*返回的**IoGetDmaAdapter**或驱动程序的设备的传输功能，二者的限制性更强，确定是否驱动程序必须拆分给定的传输请求和执行多个在其设备，以满足该 IRP 的 DMA 操作。

返回的适配器对象指针、 驱动程序的入口点*AdapterControl*例程*DeviceObject*指针来表示目标设备的当前 IRP，*上下文*指针，指向已设置了一个区域*AdapterControl*例程，和一个*NumberOfMapRegisters*小于最大可能值，该值可以是数字的较小转移请求，必须对的调用中传递[ **AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)。 通常情况下，驱动程序的[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio) (或可能[ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)) 的区域设置例程*上下文*调用之前**AllocateAdapterChannel**。

 

 




