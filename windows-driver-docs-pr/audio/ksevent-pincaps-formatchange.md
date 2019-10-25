---
title: KSEVENT\_PINCAPS\_FORMATCHANGE
description: KSEVENT\_PINCAPS\_FORMATCHANGE 事件向音频堆栈表明音频设备的音频数据格式已更改。
ms.assetid: ca9ee246-7fca-42df-89e0-7ace6b1f808a
keywords:
- KSEVENT_PINCAPS_FORMATCHANGE 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_PINCAPS_FORMATCHANGE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb5a4119f2ebcf9ba08a9b90b5d3a77c1491d29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833145"
---
# <a name="ksevent_pincaps_formatchange"></a>KSEVENT\_PINCAPS\_FORMATCHANGE


`KSEVENT_PINCAPS_FORMATCHANGE` 事件向音频堆栈表明音频设备的音频数据格式已更改。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标</th>
<th align="left">事件描述符类型</th>
<th align="left">事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型（操作数据）是指定要用于此事件的通知方法的**KSEVENTDATA**结构。

<a name="remarks"></a>备注
-------

当音频端口驱动程序为其微型端口驱动程序调用[**EventHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)例程时，它会传递一个[**PCEVENT\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)结构。 此结构包含指向[**PCEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)结构的指针，该结构用于描述筛选器、pin 或节点所支持的事件。

例如，支持 `KSEVENT_PINCAPS_FORMATCHANGE` 事件的驱动程序必须按如下所示填充**PCEVENT\_项**结构：

```cpp
static PCEVENT_ITEM FormatChangePinEvent[] = {
  {
    &KSEVENTSETID_PinCapsChange,
    KSEVENT_PINCAPS_FORMATCHANGE,
    KSEVENT_TYPE_ENABLE | KSEVENT_TYPE_BASICSUPPORT,
    MyEventHandler
  }
};
```

在上面的代码示例中，MyEventHandler 自定义事件处理程序必须监视 `KSEVENT_PINCAPS_FORMATCHANGE` 事件并在触发 KSEVENT\_PINCAPS\_FORMATCHANGE 时将其注册到 Portcls。 微型端口驱动程序必须调用[**IPortEvents：： AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist)方法来注册事件。

若要获取微型端口驱动程序支持的 pin、节点、连接和属性的说明，端口驱动程序将调用[**IMiniport：： GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)方法。 此方法调用返回一个[**PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)结构，该结构指向自动化表（[**PCAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)）。 **PCAUTOMATION\_表**结构包含**事件**成员。 此成员指向与微型端口驱动程序所支持的筛选器相关联的事件的数组。 因此，您必须将**Events**成员设置为指向事件数组，该数组包含 `KSEVENT_PINCAPS_FORMATCHANGE` 事件的**PCEVENT\_项**结构。

当微型端口驱动程序检测到动态格式更改时，它必须调用[**IPortEvents：： GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)方法来向 `KSEVENT_PINCAPS_FORMATCHANGE` 事件发出信号。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**EventHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)

[**IMiniport：： GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)

[**IPortEvents::AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist)

[**IPortEvents::GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)

[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**PCAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)

[**PCEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)

[**PCEVENT\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)

[**PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)

 

 






