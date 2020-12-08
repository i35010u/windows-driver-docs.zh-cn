---
title: 为公用缓冲区 DMA 设置系统 DMA 控制器
description: 为公用缓冲区 DMA 设置系统 DMA 控制器
keywords:
- 系统 DMA WDK 内核，公共缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，公共缓冲区
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f73948ca5ad0e69ca6a576fcf06c01fb49be4224
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837967"
---
# <a name="setting-up-the-system-dma-controller-for-common-buffer-dma"></a>为公用缓冲区 DMA 设置系统 DMA 控制器





当 **AllocateAdapterChannel** 将控制权移交给驱动程序的 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control) 例程时，驱动程序 "拥有" 系统 DMA 控制器和一组映射寄存器。 然后，驱动程序必须调用 [**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) ，将系统 DMA 控制器设置为在驱动程序设置其设备以执行传输操作之前使用驱动程序分配的公用缓冲区。

驱动程序将以下参数提供给 **MapTransfer**：

-   **IoGetDmaAdapter** 返回的适配器对象指针

-   指向描述驱动程序分配的公用缓冲区的 MDL 的指针

-   通过 **AllocateAdapterChannel** 传递到驱动程序的 *AdapterControl* 例程的 *MapRegisterBase* 句柄

-   指向变量的指针 (*长度*) 指示驱动程序分配的公共缓冲区的大小（以字节为单位）

-   一个布尔值，指示从系统内存到设备的请求传输 (TRUE 的传输操作方向) 

**MapTransfer** 返回一个逻辑地址，使用系统 DMA 的驱动程序必须忽略。 当 **MapTransfer** 返回 control 时，驱动程序应为 DMA 操作设置其设备。 驱动程序只调用一次 **MapTransfer** ，但会继续在公共缓冲区和锁定的用户缓冲区之间复制数据，直到请求的传输完成。

驱动程序可以调用 [**ReadDmaCounter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter) 来确定要在公共缓冲区中传输的当前剩余字节数;然后，该驱动程序可以继续用用户数据填充其公共缓冲区，或根据 DMA 操作的方向将数据从其公共缓冲区复制到用户缓冲区。

当传输完成或驱动程序必须为 IRP 返回错误状态时，驱动程序将调用 [**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，以确保将系统 DMA 控制器中缓存的所有数据读入系统内存或写出到设备。 然后，驱动程序应立即调用 [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) ，以释放系统 DMA 控制器以供任何驱动程序使用， (包括自身) 。

 

