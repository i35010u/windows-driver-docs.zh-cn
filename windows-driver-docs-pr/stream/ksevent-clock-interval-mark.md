---
title: KSEVENT\_时钟\_间隔\_标记
description: 客户端启用 KSEVENT\_时钟\_间隔\_后获得通知时达到初始时间值，然后在固定的时间增量的标记事件。
ms.assetid: 5292606e-d0b3-4e64-a236-c1cecf3fd53a
keywords:
- KSEVENT_CLOCK_INTERVAL_MARK 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_INTERVAL_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d68113c0a816febb25949c9c4ad91fe10e424122
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546248"
---
# <a name="kseventclockintervalmark"></a>KSEVENT\_时钟\_间隔\_标记


客户端启用 KSEVENT\_时钟\_间隔\_后获得通知时达到初始时间值，然后在固定的时间增量的标记事件。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-ideventdataspanspan-ideventdataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>事件数据

使用类型的结构[ **KSEVENT\_时间\_间隔**](https://msdn.microsoft.com/library/windows/hardware/ff561887)作为*OutBuffer*参数调用时[ **KsSynchronousDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff567142)注册此事件。

<a name="remarks"></a>备注
-------

有关如何注册事件的信息，请参阅[KS 事件](https://msdn.microsoft.com/library/windows/hardware/ff567643)。

 

 





