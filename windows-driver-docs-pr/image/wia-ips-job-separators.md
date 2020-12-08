---
title: WIA \_ IP \_ 作业 \_ 分隔符
description: "\"WIA \\_ IPS \\_ 作业 \\_ 分隔符\" 属性用于启用作业分隔符的检测，并配置设备在检测到作业分隔符页时执行的操作。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_JOB_SEPARATORS 图像设备
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
ms.openlocfilehash: 37a98d91dc3909716a119bb6b15a227cfb95e997
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825977"
---
# <a name="wia_ips_job_separators"></a>WIA \_ IP \_ 作业 \_ 分隔符


" **WIA \_ IPS \_ 作业 \_ 分隔符** " 属性用于启用作业分隔符的检测，并配置设备在检测到作业分隔符页时执行的操作。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ ip \_ 作业 \_ 分隔符** " 属性的有效值。

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
<td><p>已禁用作业分隔符检测。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SEPARATOR_DETECT_SCAN_CONTINUE</p></td>
<td><p>"检测作业分隔符" 页，扫描分隔符页，然后继续扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_SEPARATOR_DETECT_SCAN_STOP</p></td>
<td><p>"检测作业分隔符" 页，扫描分隔符页，然后停止扫描。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SEPARATOR_DETECT_NOSCAN_CONTINUE</p></td>
<td><p>"检测作业分隔符" 页上，不要扫描 (跳过) 分隔符 "页，然后继续扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_SEPARATOR_DETECT_NOSCAN_STOP</p></td>
<td><p>"检测作业分隔符" 页上，不扫描 (跳过) 分隔符 "页，然后停止扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的，仅对作为 WIA 类别送纸器) 在 [**wia \_ IPA \_ 项 \_ 类别**](wia-ipa-item-category.md) 属性中表示的送料器数据源 (项有效 \_ \_ 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





