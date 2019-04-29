---
title: 为公用缓冲区 DMA 设置系统 DMA 控制器
description: 为公用缓冲区 DMA 设置系统 DMA 控制器
ms.assetid: 279776e0-dead-4763-9aae-33950837c27c
keywords:
- 系统 DMA WDK 内核，常见的缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，常见的缓冲区
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3efbc81a2c54cd51ffdf085deaf1576fe6d96bfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367949"
---
# <a name="setting-up-the-system-dma-controller-for-common-buffer-dma"></a>为公用缓冲区 DMA 设置系统 DMA 控制器





当**AllocateAdapterChannel**将控制转移到的驱动程序[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程，该驱动程序"拥有"系统 DMA 控制器和一系列映射寄存器。 然后，该驱动程序必须调用[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)若要设置系统 DMA 控制器使用驱动程序分配的常见缓冲区，然后在传输操作其设备驱动程序设置。

驱动程序提供的以下参数**MapTransfer**:

-   所返回的适配器对象指针**IoGetDmaAdapter**

-   指向描述驱动程序分配的常见缓冲区 MDL

-   *MapRegisterBase*句柄传递给驱动程序的*AdapterControl*例程通过**AllocateAdapterChannel**

-   指向一个变量 (*长度*)，指示以字节为单位的驱动程序分配的常见缓冲区的大小

-   一个布尔值，指示在传输操作 (为 TRUE，从系统内存的请求传输到设备) 的方向

**MapTransfer**返回逻辑地址，使用系统的驱动程序必须忽略 DMA。 当**MapTransfer**返回控件，该驱动程序应设置为 DMA 操作其设备。 驱动程序调用**MapTransfer**仅一次但继续将复制其常见缓冲区和锁定的用户缓冲区之间的数据，直到完成请求的传输。

该驱动程序可以调用[ **ReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff560782)来确定多少个字节当前仍在常见的缓冲区中传输; 驱动程序可继续使用用户数据或复制数据来填充其常见的缓冲区从用户缓冲区，具体取决于 DMA 操作的方向为其常见缓冲区。

当已完成传输或驱动程序必须为 IRP 返回了错误状态，该驱动程序会调用[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)要确保任何数据缓存在系统 DMA 控制器读入系统内存或写出到设备。 然后，驱动程序应调用[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)立即以释放系统 DMA 控制器使用由任何驱动程序 （包括其本身）。

 

 




