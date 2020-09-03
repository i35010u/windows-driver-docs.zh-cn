---
title: 使用 BUS_INTERFACE_STANDARD 访问内存
description: 使用 BUS_INTERFACE_STANDARD 界面访问 PCMCIA 属性内存
ms.assetid: 2696a9ca-38b5-47f2-9639-029bba1173b5
keywords:
- 属性内存 WDK PCMCIA 总线，BUS_INTERFACE_STANDARD 接口
- BUS_INTERFACE_STANDARD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68ee12e234577a47088b98d78944fe2d37738ad3
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385105"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-bus_interface_standard-interface"></a>使用总线 \_ 接口标准界面访问 PCMCIA 属性内存 \_





本部分介绍 PC 卡或 CardBus 卡驱动程序如何使用总线 \_ 接口 \_ 标准接口访问属性内存。

\_ \_ 如果无法接受 i/o 请求的开销，驱动程序应使用总线接口标准接口。 此方法类似于 i/o 请求方法，因为它传递了一个缓冲区指针。 但是，此方法调用了一个接口例程，从而消除了 i/o 请求的开销。 如果驱动程序在以 IRQL 调度级别运行时访问属性内存，则必须使用此方法 \_ ，例如，在延迟的过程调用中 (DPC) 。

在 IRQL = DISPTACH 级别运行时，驱动程序可以使用此方法 &lt; \_ 。

驱动程序在初始化过程中通常会获得一个总线 \_ 接口 \_ 标准接口。 驱动程序使用 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) 请求从 PCMCIA 总线驱动程序获取接口。 必须以 IRQL 被动级别发送查询接口请求 \_ 。

驱动程序获取标准总线接口后，驱动程序可以调用接口例程 **GetBusData** 或 **SetBusData** 来访问属性内存。

 

