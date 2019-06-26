---
title: AdapterControl 例程的存储要求
description: AdapterControl 例程的存储要求
ms.assetid: 5e5711df-9acd-4ac5-b6b2-4e90299afb24
keywords:
- AdapterControl 例程存储
- AdapterControl 例程编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
- 存储 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb3266a369cb1f15d33b0b1654536bd742a3da7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382976"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl 例程的存储要求





如果它具有[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)例程，驱动程序必须提供常驻存储以下：

-   若要在其 DMA 操作中使用的上下文信息

-   返回一个适配器对象指针[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)

-   ULONG 类型变量来保存系统确定最大*NumberOfMapRegisters*适用于任何给定的 DMA 传输请求

该驱动程序可以提供必要的存储在设备扩展、 在控制器扩展中，或由驱动程序分配的非分页缓冲池。

 

 




