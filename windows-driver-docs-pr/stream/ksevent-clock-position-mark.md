---
title: KSEVENT\_时钟\_位置\_标记
description: 当达到某个时钟上的特定时间时，KSEVENT\_时钟\_位置\_MARK 事件发生。
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
ms.openlocfilehash: b7b231c62b0acfd1bdf3ed4119ca085739a39406
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845522"
---
# <a name="ksevent_clock_position_mark"></a>KSEVENT\_时钟\_位置\_标记


当达到某个时钟上的特定时间时，KSEVENT\_时钟\_位置\_MARK 事件发生。

### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

调用[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件时，请使用类型为[**KSEVENT\_TIME 的结构\_标记**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_mark)为*OutBuffer*参数。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅[KS 事件](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)。

 

 





