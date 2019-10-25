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
ms.openlocfilehash: bac0441655c2d251aa8a4035eec3ab034ecbb115
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838424"
---
# <a name="setting-up-adaptercontrol-routines"></a>设置 AdapterControl 例程





PnP [**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求的驱动程序调度例程必须为[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程执行以下操作：

1.  通过填写[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)结构并调用[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来设置设备 DMA 功能的适配器对象。

2.  保存**IoGetDmaAdapter**返回的适配器对象指针和*NumberOfMapRegisters* 。

    由**IoGetDmaAdapter**或驱动程序的设备的传输功能返回的特定于平台的最大*NumberOfMapRegisters*决定了该驱动程序是否必须拆分给定的传输请求并在其设备上执行多个 DMA 操作来满足 IRP。

返回的适配器对象指针，驱动程序的*AdapterControl*例程的入口点，表示当前 IRP 的目标设备的*DeviceObject*指针，该指针指向已为其*设置的区域的上下文指针。AdapterControl*例程和*NumberOfMapRegisters*值（可小于较小传输请求的最大可能数量）必须传入对[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)的调用。 通常，驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) （或可能[*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)）例程在调用**AllocateAdapterChannel**之前，在*上下文*中设置区域。

 

 




