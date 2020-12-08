---
title: KS 事件
description: KS 事件
keywords:
- 内核流 WDK，事件
- KS WDK，事件
- 事件 WDK 内核流式处理
- 事件集 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b14e89e0bf6aa4bc4c6a922cb629b64a60743de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837871"
---
# <a name="ks-events"></a>KS 事件





如果要编写 AVStream 微型驱动程序，请参阅 [AVStream 中的事件处理](event-handling-in-avstream.md)。

事件集是侦听器可以为其请求通知的相关事件的组。 例如，侦听器可以注册以接收设备状态更改或流位置更改的通知。 事件发生时，内核流式处理会通知任何已注册了此事件的客户端。

微型驱动程序介绍了如何通过提供包含指向处理例程的指针的 [**KSEVENT \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item) 结构来支持事件。

侦听器 [**通过使用 IOCTL**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol) \_ KS \_ 启用 \_ 事件控制代码并指向 [**KSEVENT**](/previous-versions/ff561744(v=vs.85)) 和 [**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)的指针，来注册通知。

IOCTL \_ KS \_ DISABLE \_ 事件请求禁用指定的事件。 用于启用事件的同一个指针必须用于禁用该事件。 此指针唯一标识事件。 或者，客户端可以指定 **NULL** 指针和零长度，以禁用客户端的所有活动事件。

所有事件集必须支持 KSEVENT \_ 类型 \_ BASICSUPPORT 标志。 有关可用事件标志的列表，请参阅 [**KSEVENT**](/previous-versions/ff561744(v=vs.85)) 。

某些事件类型需要其他参数来注册事件通知。 例如，当时钟达到某个时间戳时，将触发时钟上的 [**KSEVENT \_ 时钟 \_ 位置 \_ 标记**](./ksevent-clock-position-mark.md) 事件。 因此，注册为通知此事件的客户端必须指定触发事件的时间戳。

在这种情况下，微型驱动程序在 [**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata) 结构后传递数据缓冲区中的其他数据参数。 支持此类事件类型的微型驱动程序使用扩展的数据结构，其中第一个成员的类型为 KSEVENTDATA，用于保存通知数据。

 

