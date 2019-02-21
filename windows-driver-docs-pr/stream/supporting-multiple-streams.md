---
title: 支持多个流
description: 支持多个流
ms.assetid: 89f79078-129a-44cc-8b7e-5f5c1c33a473
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，多个流
- 流式处理微型驱动程序 WDK Windows 2000 内核，多个流
- 微型驱动程序 WDK Windows 2000 内核流式处理，多个流
- 多个流 WDK 流式处理微型驱动程序
- 支持流式处理微型驱动程序 WDK 流号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 460dc4969c5937ba7a8b67461624e5e67328a9f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547987"
---
# <a name="supporting-multiple-streams"></a>支持多个流





微型驱动程序描述它支持的流及其[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)例程，以响应 SRB\_获取\_流\_信息请求。 **CommandData.StreamBuffer**指向[ **HW\_流\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff559686)微型驱动程序应填充中使用的结构它支持的流的说明。

HW\_流\_描述符结构开头[ **HW\_流\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff559690)结构，其中描述了流的数量微型驱动程序支持。 它由一系列后接[ **HW\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff559692)结构，其中每个描述各个流。 类驱动程序将使用每个 HW\_流\_信息来处理[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)属性集 − 中数组的索引作为 pin 类型 id。

对于大多数微型驱动程序的 HW 中的数据\_流\_描述符在编译时固定。 在这种情况下，微型驱动程序可以以静态方式分配数据结构。

微型驱动程序描述其流通过硬件拓扑成员之间的连接的拓扑\_流\_标头。 类驱动程序使用此结构来处理[KSPROPSETID\_拓扑](https://msdn.microsoft.com/library/windows/hardware/ff566598)属性设置的微型驱动程序。

 

 




