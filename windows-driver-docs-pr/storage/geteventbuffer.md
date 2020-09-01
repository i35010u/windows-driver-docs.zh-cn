---
title: GetEventBuffer 函数
description: GetEventBuffer WMI 方法检索 HBA 的事件队列中的下一个事件。
ms.assetid: 9eee93e0-2661-4777-8c02-a87c4e1d744c
keywords:
- GetEventBuffer 函数存储设备
topic_type:
- apiref
api_name:
- GetEventBuffer
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c1f3da6de847fadfbe9abf9a481c332f3f0779c7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185453"
---
# <a name="geteventbuffer-function"></a>GetEventBuffer 函数


**GetEventBuffer** WMI 方法检索 HBA 的事件队列中的下一个事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetEventBuffer(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS         HBAStatus,
   [out] uint32                                    EventCount,
   [out, WmiSizeIs("EventCount")] MSFC_EventBuffer Events[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**GetEventBuffer \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)结构的**HBAStatus**成员中返回此信息。

*EventCount*   
返回时，指示检索其信息的事件数。 微型端口驱动程序在[**GetEventBuffer \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)结构的**EventCount**成员中返回此信息。

*事件\[\]*   
[**MSFC \_ EventBuffer**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)类型的结构的数组，其中包含有关 HBA 事件队列中的下一个事件的信息。 微型端口驱动程序在[**GetEventBuffer \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)结构的**Events**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

**GetEventBuffer**方法会在检索其信息后从队列中删除事件。

此 WMI 方法属于 [MSFC \_ HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">“桌面”</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetEventBuffer \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)

[**MSFC \_ EventBuffer**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

 

