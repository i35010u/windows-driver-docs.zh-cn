---
title: 设置 AdapterControl 例程
description: 设置 AdapterControl 例程
ms.assetid: 0d2add25-711a-4e5d-8409-b7ce60b08858
keywords:
- AdapterControl 例程，设置
- AdapterControl 例程，编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24af5feeeb4b7b105e10a1ddcaf41244051ef859
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184099"
---
# <a name="setting-up-adaptercontrol-routines"></a>设置 AdapterControl 例程





对于[*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程，驱动程序的 PnP [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md)请求必须执行以下操作：

1.  通过填写 [**设备 \_ 说明**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description) 结构并调用 [**IOGETDMAADAPTER**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来设置设备 DMA 功能的适配器对象。

2.  保存**IoGetDmaAdapter**返回的适配器对象指针和*NumberOfMapRegisters* 。

    由**IoGetDmaAdapter**或驱动程序的设备的传输功能返回的特定于平台的最大*NumberOfMapRegisters* ，它确定驱动程序是否必须拆分给定的传输请求并在其设备上执行多个 DMA 操作来满足 IRP。

返回的适配器对象指针、驱动程序的*AdapterControl*例程的入口点、代表当前 IRP 的目标设备的*DeviceObject*指针、指向已为*AdapterControl*例程设置的区域的*上下文*指针，以及一个*NumberOfMapRegisters*值（该值可以小于较小的传输请求的最大可能数量），必须传入对[**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)的调用。 通常，驱动程序的[*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) (或可能[*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)的) 例程在调用**AllocateAdapterChannel**之前，在*上下文*中设置区域。

 

