---
title: WIA\_IPS\_ALARM
description: WIA\_IPS\_警报属性用于配置有声警报 （蜂鸣） 中时送纸器项上实现此属性的以下条件之一的设备上的 WIA 微型驱动程序生成的 (WIA\_类别\_送纸器)，并启用多源的检测，当检测到多个源的条件时，应由设备播放有声警报 （蜂鸣） 声音。 (当 WIA\_IP\_多\_支持的源属性并将其设置为一个值，不是 WIA\_多\_馈送\_检测\_禁用，则意味着该多源检测已启用。）条形码读取器项上时实现此属性 (WIA\_类别\_条形码\_读取器)，并启用条形码检测，当条形码时，应由设备播放有声警报 （蜂鸣） 声音已成功检测到。 修补程序代码读取器项上时实现此属性 (WIA\_类别\_修补\_代码\_读取器)，并启用了修补程序代码检测，应由设备播放有声警报 （蜂鸣） 声音时已成功检测到修补程序代码。
ms.assetid: A029F7CD-C057-43FA-83AF-4B47B5A76B3F
keywords:
- WIA_IPS_ALARM 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ALARM
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8287e9e4a8aa57840113e8c7a8e1fabc1d1e7a81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546775"
---
# <a name="wiaipsalarm"></a>WIA\_IPS\_ALARM


**WIA\_IPS\_警报**属性用于配置生成的在中以下条件之一的设备驱动程序 WIA 最小化有声警报 （蜂鸣）：

-   送纸器项上时实现此属性 (WIA\_类别\_送纸器)，并启用多源的检测，当检测到多个源的条件时，应由设备播放有声警报 （蜂鸣） 声音。 (当 WIA\_IP\_多\_支持的源属性并将其设置为一个值，不是 WIA\_多\_馈送\_检测\_禁用，则意味着该多源检测已启用。）
-   条形码读取器项上时实现此属性 (WIA\_类别\_条形码\_读取器)，并启用条形码检测，当条形码成功时，应由设备播放有声警报 （蜂鸣） 声音检测到。
-   修补程序代码读取器项上时实现此属性 (WIA\_类别\_修补\_代码\_读取器)，并启用了修补程序代码检测，应由设备播放有声警报 （蜂鸣） 声音时已成功检测到修补程序代码。

此属性已初始化并维护 WIA 微型驱动程序，并且可与 Windows 8 和更高版本的 Windows。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读写

<a name="remarks"></a>备注
-------

下表中显示此属性的有效值。

| 值              | 描述                                           |
|--------------------|-------------------------------------------------------|
| WIA\_警报\_NONE   | 在设备上，将会播放 （蜂鸣） 没有有声警报。      |
| WIA\_ALARM\_BEEP1  | 在设备上，将会播放声音警报发出 （蜂鸣）。      |
| WIA\_ALARM\_BEEP2  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP3  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP4  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP5  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP6  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP7  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP8  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP9  | 另一个有声警报 （蜂鸣） 会在设备上播放。 |
| WIA\_ALARM\_BEEP10 | 另一个有声警报 （蜂鸣） 会在设备上播放。 |

 

WIA 微型驱动程序可以实现一个或多个 WIA\_警报\_提示音值，每个不同的蜂鸣声或设备支持的信号。 如果设备仅可以生成一个蜂鸣声，WIA 微型驱动程序必须仅实现 WIA\_警报\_NONE 和 WIA\_警报\_BEEP1 值。

此属性是否有效且对于送纸器项是可选的 (WIA\_类别\_送纸器) 时 WIA\_IPS\_多\_支持源属性。 此属性也是有效的和可选的条形码读取器 (WIA\_类别\_条形码\_读取器) 和修补程序代码读取器 (WIA\_类别\_PATCH\_代码\_读取器） 项。 实现此属性时，WIA\_警报\_NONE 值是必需的必须设置为默认值最小化驱动程序。

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

 

 





