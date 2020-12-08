---
title: KSEVENT \_ 时钟 \_ 位置 \_ 标记
description: '\_ \_ \_ 当达到时钟上的特定时间时，将发生 KSEVENT 时钟位置标记事件。'
keywords:
- KSEVENT_CLOCK_POSITION_MARK 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_POSITION_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b22c103fc0581f093895ed1ab4e2287f47341a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840589"
---
# <a name="ksevent_clock_position_mark"></a>KSEVENT \_ 时钟 \_ 位置 \_ 标记


\_ \_ \_ 当达到时钟上的特定时间时，将发生 KSEVENT 时钟位置标记事件。

### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

调用 [**KsSynchronousDeviceControl**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件时，请使用 [**KSEVENT \_ 时间 \_ 标记**](/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_mark)类型的结构作为 *OutBuffer* 参数。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅 [KS 事件](./ks-events.md)。

 

