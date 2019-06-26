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
ms.openlocfilehash: f0c7256bdac73282af3c5a2c0a96004b8baf2141
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378551"
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

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含 WMI 限定符值，该值指示操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetEventBuffer\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)结构。

*EventCount*   
返回时，指示已检索到其信息的事件数。 微型端口驱动程序将返回此信息**EventCount**的成员[ **GetEventBuffer\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)结构。

*事件\[\]*    
类型的结构数组[ **MSFC\_EventBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)包含 HBA 事件队列中的下一步事件有关的信息。 微型端口驱动程序将返回此信息**事件**的成员[ **GetEventBuffer\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

**GetEventBuffer**方法从队列检索其信息后删除事件。

此 WMI 方法属于[MSFC\_HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetEventBuffer\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

 

 






