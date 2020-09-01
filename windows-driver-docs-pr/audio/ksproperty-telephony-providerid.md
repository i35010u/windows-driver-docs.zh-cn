---
title: KSPROPERTY \_ 电话服务 \_ PROVIDERID
description: '\_ \_ 音频驱动程序使用 "KSPROPERTY 电话服务 PROVIDERID" 属性将提供程序标识符关联到波形筛选器。'
ms.assetid: A2BE85E3-068B-41C1-9791-69A929ECEC5C
keywords:
- KSPROPERTY_TELEPHONY_PROVIDERID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_PROVIDERID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 045d2c44950de48f0f1f1fcaa4e7c20cce7b619c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208867"
---
# <a name="ksproperty_telephony_providerid"></a>KSPROPERTY \_ 电话服务 \_ PROVIDERID


音频驱动程序使用 " **KSPROPERTY \_ 电话服务 \_ PROVIDERID** " 属性将提供程序标识符关联到波形筛选器。

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
<td align="left"><p>否</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>UINT</p></td>
</tr>
</tbody>
</table>

 

属性值为 UINT 类型并指定提供程序 ID。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ 电话服务 \_ PROVIDERID**属性请求返回表示音频驱动程序关联到波形筛选器的提供程序 ID 的 UINT 值。

<a name="remarks"></a>备注
-------

收音机堆栈具有提供程序 ID (执行器 ID) 和调用类型 (数据包或电路交换) ，以将电话呼叫实例连接到特定的硬件路径。 此概念将继续用于与音频驱动程序通信，以便使用硬件中的哪个路径。

将通过为每个提供程序发送波形筛选器的属性来控制此硬件路径。 音频驱动程序会将提供程序 ID 关联到波形筛选器。 还将在关联的移动电话流式处理终结点上设置此提供程序 ID。 在运行时，wave 筛选器的提供程序 ID 不得更改。 音频堆栈将使用 **KSPROPERTY \_ 电话服务 \_ PROVIDERID** 属性从驱动程序查询提供程序 ID。 发现此提供程序 ID 后，对该提供程序 ID 的所有调用都将发送到特定的波形筛选器。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>客户端</p></td>
<td align="left"><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

