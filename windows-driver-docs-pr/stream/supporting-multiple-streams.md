---
title: 支持多个流
description: 支持多个流
ms.assetid: 89f79078-129a-44cc-8b7e-5f5c1c33a473
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，多个流
- 流式传输微型驱动程序 WDK Windows 2000 内核，多个流
- 微型驱动程序 WDK Windows 2000 内核流式处理，多个流
- 多流 WDK 流式处理微型驱动程序
- 流数字支持的 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c60634ec7d7e64b4d4b401fa74a5443b47aca40
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186087"
---
# <a name="supporting-multiple-streams"></a>支持多个流





微型驱动程序介绍其在 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 例程中支持的流，以响应 SRB \_ 获取 \_ 流 \_ 信息请求。 **CommandData StreamBuffer**指向[**HW \_ 流 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)结构，微型驱动程序应填写它所支持的流的说明。

HW \_ 流 \_ 描述符结构以 [**hw \_ 流 \_ 标头**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header) 结构开头，该结构描述了微型驱动程序支持的流的数量。 后跟一个 [**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information) 结构数组，其中每个结构都描述单个流。 类驱动程序使用每个 HW \_ 流 \_ 信息来处理 [KSPROPSETID \_ 引脚](./kspropsetid-pin.md) 属性集−数组中的索引用作 Pin 类型 ID。

对于大多数微型驱动程序，HW 流描述符中的数据在 \_ \_ 编译时是固定的。 在这种情况下，微型驱动程序可以静态分配数据结构。

微型驱动程序描述了其流通过 HW \_ 流标头的拓扑成员的连接拓扑 \_ 。 类驱动程序使用此结构来处理微型驱动程序的 [KSPROPSETID \_ 拓扑](./kspropsetid-topology.md) 属性集。

 

