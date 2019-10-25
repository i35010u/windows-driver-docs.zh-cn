---
title: KSEVENT\_时钟\_间隔\_标记
description: 客户端启用 KSEVENT\_时钟\_间隔，\_标记在达到初始时间值时通知事件，然后在该时间之后递增固定的时间。
ms.assetid: 5292606e-d0b3-4e64-a236-c1cecf3fd53a
keywords:
- KSEVENT_CLOCK_INTERVAL_MARK 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_INTERVAL_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb042dca53d7a76037aed9d45160ce466136db4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845524"
---
# <a name="ksevent_clock_interval_mark"></a>KSEVENT\_时钟\_间隔\_标记


客户端启用 KSEVENT\_时钟\_间隔，\_标记在达到初始时间值时通知事件，然后在该时间之后递增固定的时间。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

调用[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)注册此事件时，请使用类型为[**KSEVENT\_时间\_间隔**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_interval)的结构作为*OutBuffer*参数。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅[KS 事件](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)。

 

 





