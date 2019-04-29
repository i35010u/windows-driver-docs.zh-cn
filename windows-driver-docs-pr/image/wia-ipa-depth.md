---
title: WIA\_IPA\_DEPTH
description: WIA\_IPA\_DEPTH 属性包含位深度设置的图像的区域设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 90f7983c-296f-4dfc-90d3-886881a907af
keywords:
- WIA_IPA_DEPTH 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_DEPTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd89ae491a066af635f902ee973b864c98c86300
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369548"
---
# <a name="wiaipadepth"></a>WIA\_IPA\_DEPTH


WIA\_IPA\_DEPTH 属性包含位深度设置的图像的区域设置。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPA\_DEPTH 属性来确定图像的位深度设置。 应用程序还可能会设置此属性为所需的位深度或 WIA\_深度\_自动值。

如果可以将设备设置一个值，创建 WIA\_PROP\_列表类型并将有效的值放入其中。

WIA\_深度\_（定义为 0 位 / 像素） 的自动值是否有效的所有可编程图像数据源项，包括平板和送纸器。 此值的 WIA 微型驱动程序 WIA 应用程序客户端的支持时可以设置**WIA\_IPA\_深度**为以便在设备上的自动颜色检测此值。

当**WIA\_IPA\_深度**属性设置为 WIA\_深度\_自动，WIA 微型驱动程序必须更新[ **WIA\_IPA\_数据类型**](wia-ipa-datatype.md) WIA 的同一个项上的属性\_数据\_自动 （它必须是受支持的值，如果设备支持的自动颜色）。 当**WIA\_IPA\_数据类型**值 WIA\_数据\_支持自动，则**WIA\_IPA\_深度**值WIA\_深度\_自动不再是可选的将成为所需的值。

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

 

 





