---
title: WIA\_IPS\_打印机\_印记签署器\_字体\_类型
description: WIA\_IPS\_打印机\_印记签署器\_字体\_类型属性配置打印机/印记签署器设备使用的字体类型。
ms.assetid: DBA20346-36F8-4D9A-A9F2-F97F8955CDF8
keywords:
- WIA_IPS_PRINTER_ENDORSER_FONT_TYPE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_FONT_TYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92a1d065a6281a68782511fe9441b091dae761e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562805"
---
# <a name="wiaipsprinterendorserfonttype"></a>WIA\_IPS\_打印机\_印记签署器\_字体\_类型


**WIA\_IPS\_打印机\_印记签署器\_字体\_类型**属性配置打印机/印记签署器设备使用的字体类型。 此属性是初始化和维护的 WIA 微型驱动程序。 与 Windows 8 和更高版本的 Windows 提供了此功能。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读写

<a name="remarks"></a>备注
-------

接受的值**WIA\_IPS\_打印机\_印记签署器\_字体\_类型**属性显示在下表中。

| ReplTest1                                        | 描述                       |
|----------------------------------------------|-----------------------------------|
| WIA\_打印\_字体\_正常                     | 正常的字体。                      |
| WIA\_打印\_字体\_加粗                       | 粗体的字体。                        |
| WIA\_打印\_字体\_额外\_加粗                | 额外加粗字体。                  |
| WIA\_打印\_字体\_斜体\_加粗               | 斜体、 粗体的字体。                |
| WIA\_打印\_字体\_斜体\_额外\_加粗        | 斜体，额外粗体的字体。          |
| WIA\_打印\_字体\_斜体                     | 倾斜字体。                      |
| WIA\_打印\_字体\_小                      | 很小的字体。                       |
| WIA\_打印\_字体\_小型\_加粗                | 很小的加粗字体。                  |
| WIA\_打印\_字体\_小型\_额外\_加粗         | 很小的额外加粗字体。            |
| WIA\_打印\_字体\_小型\_斜体\_加粗        | 小斜体和粗体的字体。       |
| WIA\_打印\_字体\_小型\_斜体\_额外\_加粗 | 很小的斜体和额外加粗字体。 |
| WIA\_打印\_字体\_小型\_斜体              | 很小的斜体字体。                |
| WIA\_打印\_字体\_大                      | 大字体。                       |
| WIA\_打印\_字体\_大\_加粗                | 大加粗字体。                  |
| WIA\_PRINT\_FONT\_LARGE\_EXTRA\_BOLD         | 大型额外粗体的字体。            |
| WIA\_打印\_字体\_LARGE\_斜体\_加粗        | 大型斜体和粗体的字体。       |
| WIA\_PRINT\_FONT\_LARGE\_ITALIC\_EXTRA\_BOLD | 大型斜体和额外加粗字体。 |
| WIA\_打印\_字体\_大\_斜体              | 大型倾斜字体。                |

 

**WIA\_IPS\_打印机\_印记签署器\_字体\_类型**属性是可选的印刷器/印记签署器项。 如果不支持这样做，打印机/印记签署器设备不支持字体配置。

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

 

 





