---
title: KSPROPERTY \_ AEC \_ 模式
description: KSPROPERTY \_ aec \_ 模式属性用于控制 aec 节点的操作模式。 这是 AEC 节点的一个可选属性， (KSNODETYPE \_ \_ 的声音回声 \_ 取消) 。
ms.assetid: 79f0d655-4764-454f-8867-6cf1b5cedc82
keywords:
- KSPROPERTY_AEC_MODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40907367801e55a8285569eff12a275775b598a3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102324"
---
# <a name="ksproperty_aec_mode"></a>KSPROPERTY \_ AEC \_ 模式


KSPROPERTY \_ aec \_ 模式属性用于控制 aec 节点的操作模式。 这是 AEC 节点的一个可选属性， ([**KSNODETYPE 的 \_ 声音 \_ 回声 \_ 取消**](ksnodetype-acoustic-echo-cancel.md)) 。

## <span id="ddk_ksproperty_aec_mode_ks"></span><span id="DDK_KSPROPERTY_AEC_MODE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">获取</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，可以设置为标头文件 Ksmedia 中的以下模式常量之一：

-   AEC \_ 模式 \_ 经过 \_

    在直通模式下，AEC 节点允许捕获和呈现数据，以便在不进行修改的情况下直接传递节点。

-   AEC \_ 模式 \_ 半 \_ 双工

    AEC 算法在半双工模式下运行，该模式在操作中与播音电话类似。 在此模式下，每当本地人物的语音具有比远程人员更高的音量级别时，扬声器音量就会静音。

-   AEC \_ 模式 \_ 全双工 \_

    AEC 算法在全双工模式下运行。

传递模式为默认值。 当创建包含 AEC 节点的筛选器或重置节点时，该节点最初配置为在传递模式下运行。

在 Windows XP 的初始版本中， [aec 系统筛选器](./aec-system-filter.md) 使用的 aec 算法不支持半双工模式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AEC \_ 模式属性请求返回状态 \_ SUCCESS，指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE \_ 回声 \_ \_ 取消**](ksnodetype-acoustic-echo-cancel.md)

