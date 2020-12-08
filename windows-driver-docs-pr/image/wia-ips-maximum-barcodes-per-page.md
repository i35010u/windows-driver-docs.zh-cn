---
title: WIA \_ IPS \_ \_ \_ 每页最大条形码 \_
description: "\"WIA \\_ IPS \\_ \\_ 每页最大条形码 \\_ 数\" \\_ 属性描述启用了条形码检测时，设备可以并在一个文档页端检测到的最大条形码数量。"
keywords:
- WIA_IPS_MAXIMUM_BARCODES_PER_PAGE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_BARCODES_PER_PAGE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4f20cfcd3dd8b726922feda78531c2c79e7c1c44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840701"
---
# <a name="wia_ips_maximum_barcodes_per_page"></a>WIA \_ IPS \_ \_ \_ 每页最大条形码 \_


" **WIA \_ IPS \_ \_ \_ 每 \_ 页最大条形码** 数" 属性描述启用了条形码检测时，设备可以并在一个文档页端检测到的最大条形码数量。




属性类型： VT \_ UI4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

值0表示 "无最大值"。 应用程序可以减小此属性的当前值，以便缩短用于条形码检测的时间，并提高扫描速度。

此属性对所有条码读取器项都是必需的，但它可以作为范围容器来实现，该容器只包含 0 (最小值等于并设置为0，步长大小为 0) 。

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

 

 





