---
title: WIA\_IPS\_作业\_分隔符
description: WIA\_IPS\_作业\_分隔符属性用于启用作业分隔符，检测并配置设备时检测到作业分隔页执行的操作。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 2ECD88EB-2B6F-477D-8F37-D4EECA580FAE
keywords:
- WIA_IPS_JOB_SEPARATORS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_JOB_SEPARATORS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c3dfb8a5f462f1374761fe5bea27fd3b6fc64d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564693"
---
# <a name="wiaipsjobseparators"></a>WIA\_IPS\_作业\_分隔符


**WIA\_IPS\_作业\_分隔符**属性来启用的作业的分隔符，检测并配置设备时检测到作业分隔页执行的操作。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_作业\_分隔符**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_SEPARATOR_DISABLED</p></td>
<td><p>禁用作业分隔符检测。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SEPARATOR_DETECT_SCAN_CONTINUE</p></td>
<td><p>检测作业分隔页、 扫描分隔符页上，并继续扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_SEPARATOR_DETECT_SCAN_STOP</p></td>
<td><p>检测作业分隔页、 扫描分隔符页上，并停止扫描。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SEPARATOR_DETECT_NOSCAN_CONTINUE</p></td>
<td><p>检测作业分隔页、 不扫描 （跳过） 分隔符页上，并继续扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_SEPARATOR_DETECT_NOSCAN_STOP</p></td>
<td><p>检测作业分隔页、 不扫描 （跳过） 分隔符页上，并停止扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的并且仅对送纸器数据源项有效 (以表示[ **WIA\_IPA\_项\_类别**](wia-ipa-item-category.md)属性作为 WIA\_类别\_送纸器)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





