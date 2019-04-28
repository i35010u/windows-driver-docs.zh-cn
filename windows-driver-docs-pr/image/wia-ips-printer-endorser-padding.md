---
title: WIA\_IPS\_打印机\_印记签署器\_填充
description: WIA\_IPS\_打印机\_印记签署器\_PADDING 属性配置打印或认可来填充空格计数器中的有效特殊填充字符的日期和时间序列。
ms.assetid: 44C8A517-43E5-4986-9B8A-46167B5884E5
keywords:
- WIA_IPS_PRINTER_ENDORSER_PADDING 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_PADDING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f52676394c3e28b56f5ed15195225a4d46171c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351139"
---
# <a name="wiaipsprinterendorserpadding"></a>WIA\_IPS\_打印机\_印记签署器\_填充


**WIA\_IPS\_打印机\_印记签署器\_填充**属性配置的有效特殊填充字符的打印或认可来填充计数器，数据中的空格和时间序列。 此属性已初始化并维护 WIA 微型驱动程序，并且可与 Windows 8 和更高版本的 Windows。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读写

<a name="remarks"></a>备注
-------

下表中显示此属性的有效值。

| 值                      | 描述                                        |
|----------------------------|----------------------------------------------------|
| WIA\_打印\_PADDING\_NONE  | 无需进行填充。                                        |
| WIA\_PRINT\_PADDING\_ZERO  | 零 (0) 数字用作填充字符。 |
| WIA\_PRINT\_PADDING\_BLANK | 空白 （空） 字符用于填充。   |

 

**WIA\_IPS\_打印机\_印记签署器\_填充**属性是可选的印刷器/印记签署器项。 如果不支持此属性，打印机/印记签署器设备不支持填充。

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

 

 





