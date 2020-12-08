---
title: WIA \_ IP \_ 条形码 \_ 搜索 \_ 超时
description: "\"WIA \\_ ip \\_ 条形码 \\_ 搜索 \\_ 超时值\" 属性描述在文档页面上搜索条形码的最长时间。"
keywords:
- WIA_IPS_BARCODE_SEARCH_TIMEOUT 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_SEARCH_TIMEOUT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: da1a9bf7cbaad87cb93275a018abab6e16e98356
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817189"
---
# <a name="wia_ips_barcode_search_timeout"></a>WIA \_ IP \_ 条形码 \_ 搜索 \_ 超时


" **WIA \_ ip \_ 条形码 \_ 搜索 \_ 超时值** " 属性描述在文档页面上搜索条形码的最长时间。


属性类型： VT \_ UI4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

未指定时间单位 (它可以是毫秒或十分之一秒，例如) ，但是应用程序可以选择由 WIA 微型驱动程序报告的最小–最大范围内的值。

所有条形码读取器项都需要此属性。 可以实现属性以支持包含一个值的范围 (意味着应用程序无法将此超时值更改) 。

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

 

 





