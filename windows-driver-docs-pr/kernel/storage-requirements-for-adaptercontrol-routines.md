---
title: AdapterControl 例程的存储要求
description: AdapterControl 例程的存储要求
ms.assetid: 5e5711df-9acd-4ac5-b6b2-4e90299afb24
keywords:
- AdapterControl 例程，存储
- AdapterControl 例程，编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
- 存储 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9895d42dd196af2c4f26c1e63ab52f0851e73cbb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184397"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl 例程的存储要求





如果它具有 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control) 例程，则驱动程序必须为以下各项提供常驻存储：

-   要在其 DMA 操作中使用的上下文信息

-   IoGetDmaAdapter 返回的适配器对象指针[ **IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

-   一个 ULONG 类型变量，用于保存适用于任何给定 DMA 传输请求的系统确定的最大*NumberOfMapRegisters*

驱动程序可以在设备扩展、控制器扩展或驱动程序分配的非分页池中提供必要的存储。

 

