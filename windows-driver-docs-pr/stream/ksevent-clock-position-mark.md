---
title: KSEVENT \_ 时钟 \_ 位置 \_ 标记
description: '\_ \_ \_ 当达到时钟上的特定时间时，将发生 KSEVENT 时钟位置标记事件。'
ms.assetid: 489e7441-41e9-40e5-8bf5-0bff2fda9f27
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
ms.openlocfilehash: 7647fe6a271b6ac529a16bb19244d8fee8e0b8ac
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186625"
---
# <a name="ksevent_clock_position_mark"></a>KSEVENT \_ 时钟 \_ 位置 \_ 标记


\_ \_ \_ 当达到时钟上的特定时间时，将发生 KSEVENT 时钟位置标记事件。

### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

调用[**KsSynchronousDeviceControl**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件时，请使用[**KSEVENT \_ 时间 \_ 标记**](/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_mark)类型的结构作为*OutBuffer*参数。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅 [KS 事件](./ks-events.md)。

 

