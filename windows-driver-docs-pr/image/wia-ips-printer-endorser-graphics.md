---
title: WIA\_IPS\_打印机\_印记签署器\_图形
description: WIA\_IPS\_打印机\_印记签署器\_图形属性用于报告的印刷器/印记签署器项是否支持以及文本的图形和图像数据。
ms.assetid: F2550D8F-DF66-4184-909B-F0CCB68AD7C6
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e8d6874b1f1e02db8747bec06709965f8e3c85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526745"
---
# <a name="wiaipsprinterendorsergraphics"></a>WIA\_IPS\_打印机\_印记签署器\_图形


**WIA\_IPS\_打印机\_印记签署器\_图形**属性用于报告的印刷器/印记签署器项是否支持以及文本的图形和图像数据。 图形通常由设备用于打印/认可附近文本，或作为背景图像。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4 （布尔值）

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果**WIA\_IPS\_打印机\_印记签署器\_图形**提供支持，将设置为非零值 (True) 的值，印刷器/印记签署器支持图形数据。

此属性是必需的所有印刷器/印记签署器项，但它可以实现以始终报告的值为 0 (False)。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





