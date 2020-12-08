---
title: KSPROPERTY \_ 音频 \_ VOLUMELIMIT \_
description: KSPROPERTY \_ AUDIO \_ VOLUMELIMIT \_ ，它是一个新的 KS 属性，已添加到 \_ Windows 8.1 中的 KSPROPSETID 音频属性集中。
keywords:
- KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc350528b4ab6bc4be92754a41ec04f32e6ff469
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784449"
---
# <a name="ksproperty_audio_volumelimit_engaged"></a>KSPROPERTY \_ 音频 \_ VOLUMELIMIT \_


KSPROPERTY \_ AUDIO \_ VOLUMELIMIT \_ ，它是一个新的 KS 属性，已添加到 \_ Windows 8.1 中的 KSPROPSETID 音频属性集中。

KSPROPERTY \_ AUDIO \_ VOLUMELIMIT \_ 接合属性请求将最终用户的音量级别限制首选项传递给基础驱动程序。 此属性的作用域是从最终用户的角度) ，每个 pin (或每个音频端点。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>固定实例</p></td>
<td align="left"><p>KSP_PIN</p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 BOOL，它指示最终用户是否允许 max 卷超过特定限制。 如果值为 TRUE，则表示最终用户已允许卷级别超过已发布的限制，而 FALSE 表示相反。 对于子帐户，此值将始终为 FALSE。

驱动程序将此属性的值存储在内部变量中，并在启动期间将值初始化为 TRUE。 此属性为 TRUE 时，驱动程序会限制最大卷级别。 当属性设置为 FALSE 时，驱动程序可以消除这些限制。

驱动程序还可以自动更改此属性的值。 例如，驱动程序可以自动将属性值从 TRUE 转换为 FALSE，然后在特定的音量级别超过一定时间后开始限制卷级别。

每当属性的值发生更改时，无论它是自动的还是由调用方设置属性值，驱动程序都应生成 KSEVENT \_ PINCAPS \_ VOLUMELIMITCHANGE 事件。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_ \_ 请求成功时，KSPROPERTY AUDIO VOLUMELIMIT \_ 订婚属性请求返回状态 \_ 成功。

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

 





