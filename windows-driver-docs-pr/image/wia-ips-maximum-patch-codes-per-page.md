---
title: WIA \_ IPS \_ \_ \_ \_ 每 \_ 页最多修补程序代码
description: "\"WIA \\_ IPS \\_ 最大 \\_ 修补程序 \\_ 代码 \\_ （每页）\" \\_ 属性描述启用了修补程序代码检测时，设备可以并在一个文档页端检测到的修补程序代码的最大数目。"
keywords:
- WIA_IPS_MAXIMUM_PATCH_CODES_PER_PAGE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_PATCH_CODES_PER_PAGE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0a59b4ec3167cb025819b7cae802d918797def2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808191"
---
# <a name="wia_ips_maximum_patch_codes_per_page"></a>WIA \_ IPS \_ \_ \_ \_ 每 \_ 页最多修补程序代码


" **WIA \_ IPS \_ 最大 \_ 修补程序 \_ 代码（ \_ 每 \_ 页** ）" 属性描述启用了修补程序代码检测时，设备可以并在一个文档页端检测到的修补程序代码的最大数目。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

值0表示 "无最大值"。 应用程序可以减少此属性的当前值，以便缩短修补程序代码检测所用的时间并提高扫描速度。

此属性是所有修补程序代码读取器项所必需的，但它可以作为范围容器实现，该容器只包含 0 (最小值等于并设置为0，步长大小为 0) 。

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

 

 





