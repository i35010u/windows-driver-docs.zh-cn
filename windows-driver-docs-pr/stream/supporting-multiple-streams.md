---
title: 支持多个流
description: 支持多个流
ms.assetid: 89f79078-129a-44cc-8b7e-5f5c1c33a473
keywords:
- Stream .sys 类驱动程序 WDK Windows 2000 内核，多个流
- 流式传输微型驱动程序 WDK Windows 2000 内核，多个流
- 微型驱动程序 WDK Windows 2000 内核流式处理，多个流
- 多流 WDK 流式处理微型驱动程序
- 流数字支持的 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19780e8a065963f21aaa59c012fb9e3fd912ecf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837668"
---
# <a name="supporting-multiple-streams"></a>支持多个流





微型驱动程序介绍其在[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)例程中支持的流，以响应 SRB\_获取\_流\_信息请求。 **CommandData StreamBuffer**指向[**HW\_STREAM\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)结构，微型驱动程序应填写它所支持的流的说明。

HW\_STREAM\_描述符结构以[**hw\_\_stream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)开头，该结构描述了微型驱动程序支持的流数量。 后跟一组[**HW\_STREAM\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)结构，每个结构都描述单个流。 类驱动程序使用每个 HW\_流\_信息来处理[KSPROPSETID\_引脚](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)属性集−数组中的索引用作 PIN 类型 ID。

对于大多数微型驱动程序，HW\_STREAM\_描述符中的数据在编译时是固定的。 在这种情况下，微型驱动程序可以静态分配数据结构。

微型驱动程序介绍了\_标头的 HW\_流的拓扑成员的流之间的连接拓扑。 类驱动程序使用此结构来处理为微型驱动程序[\_拓扑](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)属性集设置的 KSPROPSETID。

 

 




