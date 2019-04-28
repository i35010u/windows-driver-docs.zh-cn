---
title: WIA\_IPS\_FILM\_SCAN\_MODE
description: WIA\_IPS\_电影\_扫描\_模式属性包含当前电影扫描配置设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 3bbe362e-1868-4327-a862-8711f09969f7
keywords:
- WIA_IPS_FILM_SCAN_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_FILM_SCAN_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05ec5d7bc0ae73114ee586e3ad1524ad09de00d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348293"
---
# <a name="wiaipsfilmscanmode"></a>WIA\_IPS\_FILM\_SCAN\_MODE


WIA\_IPS\_电影\_扫描\_模式属性包含当前电影扫描配置设置。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_IPS\_电影\_扫描\_模式属性

| 扫描类型                  | 定义                                         |
|----------------------------|----------------------------------------------------|
| WIA\_电影\_颜色\_幻灯片    | 扫描将颜色扫描。                     |
| WIA\_FILM\_COLOR\_NEGATIVE | 扫描将负的颜色进行扫描。       |
| WIA\_FILM\_BW\_NEGATIVE    | 扫描将黑色和白色 （灰度） 扫描。 |

 

此属性是必需的电影胶片扫描仪和透明度适配器 WIA 项树中根项。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





