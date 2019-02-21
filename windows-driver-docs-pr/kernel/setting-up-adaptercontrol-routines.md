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
ms.openlocfilehash: dab2afbd52e8b114798915c1ae64fa3d8803f128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540666"
---
# <a name="setting-up-adaptercontrol-routines"></a>设置 AdapterControl 例程





有关即插即用驱动程序的调度例程[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求必须执行以下操作[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程：

1.  设置设备的 DMA 功能的适配器对象通过填写[**设备\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff543107)结构和调用[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220).

2.  保存适配器的对象指针和*NumberOfMapRegisters*返回的**IoGetDmaAdapter**。

    特定于平台的最大*NumberOfMapRegisters*返回的**IoGetDmaAdapter**或驱动程序的设备的传输功能，二者的限制性更强，确定是否驱动程序必须拆分给定的传输请求和执行多个在其设备，以满足该 IRP 的 DMA 操作。

返回的适配器对象指针、 驱动程序的入口点*AdapterControl*例程*DeviceObject*指针来表示目标设备的当前 IRP，*上下文*指针，指向已设置了一个区域*AdapterControl*例程，和一个*NumberOfMapRegisters*小于最大可能值，该值可以是数字的较小转移请求，必须对的调用中传递[ **AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)。 通常情况下，驱动程序的[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858) (或可能[ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)) 的区域设置例程*上下文*调用之前**AllocateAdapterChannel**。

 

 




