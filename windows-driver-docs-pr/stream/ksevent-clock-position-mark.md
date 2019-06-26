---
title: KSEVENT\_时钟\_位置\_标记
description: KSEVENT\_时钟\_位置\_到达特定时间制时发生标记事件。
ms.assetid: 489e7441-41e9-40e5-8bf5-0bff2fda9f27
keywords:
- KSEVENT_CLOCK_POSITION_MARK 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_POSITION_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1faf2e794817333cb415bce67cf4c83dacc954d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382436"
---
# <a name="kseventclockpositionmark"></a>KSEVENT\_时钟\_位置\_标记


KSEVENT\_时钟\_位置\_到达特定时间制时发生标记事件。

### <a name="span-ideventdataspanspan-ideventdataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

使用类型的结构[ **KSEVENT\_时间\_标记**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_time_mark)作为*OutBuffer*参数时调用[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅[KS 事件](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)。

 

 





