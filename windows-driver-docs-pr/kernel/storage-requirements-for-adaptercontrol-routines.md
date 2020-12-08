---
title: AdapterControl 例程的存储要求
description: AdapterControl 例程的存储要求
keywords:
- AdapterControl 例程，存储
- AdapterControl 例程，编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
- 存储 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6cf2eabb76d94fd6bf70d471265fcf92e7c140
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815273"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl 例程的存储要求





如果它具有 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control) 例程，则驱动程序必须为以下各项提供常驻存储：

-   要在其 DMA 操作中使用的上下文信息

-   IoGetDmaAdapter 返回的适配器对象指针 [ **IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

-   一个 ULONG 类型变量，用于保存适用于任何给定 DMA 传输请求的系统确定的最大 *NumberOfMapRegisters*

驱动程序可以在设备扩展、控制器扩展或驱动程序分配的非分页池中提供必要的存储。

 

