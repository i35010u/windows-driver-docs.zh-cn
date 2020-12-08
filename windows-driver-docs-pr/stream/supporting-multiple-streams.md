---
title: 支持多个流
description: 支持多个流
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，多个流
- 流式传输微型驱动程序 WDK Windows 2000 内核，多个流
- 微型驱动程序 WDK Windows 2000 内核流式处理，多个流
- 多流 WDK 流式处理微型驱动程序
- 流数字支持的 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3861ece70953e6a131bad1b058d58c2654e16c30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839831"
---
# <a name="supporting-multiple-streams"></a>支持多个流





微型驱动程序介绍其在 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 例程中支持的流，以响应 SRB \_ 获取 \_ 流 \_ 信息请求。 **CommandData StreamBuffer** 指向 [**HW \_ 流 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)结构，微型驱动程序应填写它所支持的流的说明。

HW \_ 流 \_ 描述符结构以 [**hw \_ 流 \_ 标头**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header) 结构开头，该结构描述了微型驱动程序支持的流的数量。 后跟一个 [**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information) 结构数组，其中每个结构都描述单个流。 类驱动程序使用每个 HW \_ 流 \_ 信息来处理 [KSPROPSETID \_ 引脚](./kspropsetid-pin.md) 属性集−数组中的索引用作 Pin 类型 ID。

对于大多数微型驱动程序，HW 流描述符中的数据在 \_ \_ 编译时是固定的。 在这种情况下，微型驱动程序可以静态分配数据结构。

微型驱动程序描述了其流通过 HW \_ 流标头的拓扑成员的连接拓扑 \_ 。 类驱动程序使用此结构来处理微型驱动程序的 [KSPROPSETID \_ 拓扑](./kspropsetid-topology.md) 属性集。

 

