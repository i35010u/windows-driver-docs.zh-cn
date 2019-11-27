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
ms.openlocfilehash: fd27ba68c3dca1668cd9474e88a46f72e5ba051c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836232"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl 例程的存储要求





如果它具有[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程，则驱动程序必须为以下各项提供常驻存储：

-   要在其 DMA 操作中使用的上下文信息

-   IoGetDmaAdapter 返回的适配器对象指针[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

-   一个 ULONG 类型变量，用于保存适用于任何给定 DMA 传输请求的系统确定的最大*NumberOfMapRegisters*

驱动程序可以在设备扩展、控制器扩展或驱动程序分配的非分页池中提供必要的存储。

 

 




