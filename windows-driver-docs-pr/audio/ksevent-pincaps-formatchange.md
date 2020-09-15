---
title: KSEVENT \_ PINCAPS \_ FORMATCHANGE
description: KSEVENT \_ PINCAPS \_ FORMATCHANGE 事件向音频堆栈表明音频设备的音频数据格式已更改。
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
ms.openlocfilehash: 76e626f2c501068ea550848e8ed44b6ece11cb21
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102658"
---
# <a name="ksevent_pincaps_formatchange"></a>KSEVENT \_ PINCAPS \_ FORMATCHANGE


`KSEVENT_PINCAPS_FORMATCHANGE`事件向音频堆栈表明音频设备的音频数据格式已更改。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span> 使用情况摘要表

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的事件值类型是一个指定要用于此事件的通知方法的 **KSEVENTDATA** 结构。

<a name="remarks"></a>备注
-------

当音频端口驱动程序为其微型端口驱动程序调用 [**EventHandler**](/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler) 例程时，它将传递 [**PCEVENT \_ 请求**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request) 结构。 此结构包含指向 [**PCEVENT \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item) 结构的指针，该结构用于描述筛选器、pin 或节点所支持的事件。

例如，支持该事件的驱动程序 `KSEVENT_PINCAPS_FORMATCHANGE` 必须按如下所示填充 **PCEVENT \_ 项** 结构：

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

在上面的代码示例中，MyEventHandler 自定义事件处理程序必须监视 `KSEVENT_PINCAPS_FORMATCHANGE` 事件，并在触发 KSEVENT PINCAPS FORMATCHANGE 时将其注册到 Portcls \_ \_ 。 微型端口驱动程序必须调用 [**IPortEvents：： AddEventToEventList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist) 方法来注册事件。

若要获取微型端口驱动程序支持的 pin、节点、连接和属性的说明，端口驱动程序将调用 [**IMiniport：： GetDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription) 方法。 此方法调用将返回 [**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor) 结构，该结构指向 ([**PCAUTOMATION \_ 表**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)) 的自动化表。 **PCAUTOMATION \_ 表**结构包含**事件**成员。 此成员指向与微型端口驱动程序所支持的筛选器相关联的事件的数组。 因此，您必须将 **Events** 成员设置为指向事件数组，该事件数组包含事件的 **PCEVENT \_ 项** 结构 `KSEVENT_PINCAPS_FORMATCHANGE` 。

当微型端口驱动程序检测到动态格式更改时，它必须调用 [**IPortEvents：： GenerateEventList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist) 方法来向 `KSEVENT_PINCAPS_FORMATCHANGE` 事件发出信号。

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
<td align="left">Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**EventHandler**](/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)

[**IMiniport：： GetDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)

[**IPortEvents::AddEventToEventList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist)

[**IPortEvents::GenerateEventList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)

[**KSEVENT**](/previous-versions/ff561744(v=vs.85))

[**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**PCAUTOMATION \_ 表**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)

[**PCEVENT \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)

[**PCEVENT \_ 请求**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)

[**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)

