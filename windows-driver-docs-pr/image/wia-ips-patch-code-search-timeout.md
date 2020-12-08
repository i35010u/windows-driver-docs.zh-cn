---
title: WIA \_ IPS \_ 修补程序 \_ 代码 \_ 搜索 \_ 超时
description: "\"WIA \\_ IPS \\_ 修补程序 \\_ 代码 \\_ 搜索 \\_ 超时值\" 属性描述在文档页面上搜索修补程序代码的最长时间。"
keywords:
- WIA_IPS_PATCH_CODE_SEARCH_TIMEOUT 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_SEARCH_TIMEOUT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 877b7e94031be128593c9e72e0e72ab0c9921e3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839907"
---
# <a name="wia_ips_patch_code_search_timeout"></a>WIA \_ IPS \_ 修补程序 \_ 代码 \_ 搜索 \_ 超时


" **WIA \_ IPS \_ 修补程序 \_ 代码 \_ 搜索 \_ 超时值** " 属性描述在文档页面上搜索修补程序代码的最长时间。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

未指定时间单位 (例如) ，则它可以为毫秒或十分之一秒，但应用程序可以选择 WIA 微型驱动程序报告的最小–最大范围内的值。

所有修补程序代码读取器项都需要此属性。 可以实现属性，以支持包含单个值的范围 (意味着应用程序无法更改此超时值) 

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

 

 





