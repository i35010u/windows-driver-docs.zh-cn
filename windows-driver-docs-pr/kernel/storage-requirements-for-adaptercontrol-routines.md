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
ms.openlocfilehash: 4d0252a2226b844c30f7521008ccfb6beff5cc61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545223"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl 例程的存储要求





如果它具有[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程，驱动程序必须提供常驻存储以下：

-   若要在其 DMA 操作中使用的上下文信息

-   返回一个适配器对象指针[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

-   ULONG 类型变量来保存系统确定最大*NumberOfMapRegisters*适用于任何给定的 DMA 传输请求

该驱动程序可以提供必要的存储在设备扩展、 在控制器扩展中，或由驱动程序分配的非分页缓冲池。

 

 




