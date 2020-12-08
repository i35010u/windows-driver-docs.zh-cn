---
title: WIA \_ IPA \_ 深度
description: WIA \_ IPA \_ depth 属性包含图像的位深度设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_DEPTH 图像设备
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
ms.openlocfilehash: 5fe3d124cc16668cdeec08d9e559821adc025aa8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817321"
---
# <a name="wia_ipa_depth"></a>WIA \_ IPA \_ 深度


WIA \_ IPA \_ depth 属性包含图像的位深度设置。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ IPA \_ DEPTH 属性以确定图像的位深度设置。 应用程序还可以将此属性设置为所需的位深度，或设置为 WIA \_ 深度 \_ 自动值。

如果可以将设备设置为仅使用单个值，请创建一个 WIA 的 " \_ \_ 类型"，并在其中放置有效值。

WIA \_ 深度 \_ 自动值 (定义为每像素0位数) 对于所有可编程的图像数据源项（包括平板和进纸器）都有效。 当 WIA 小型驱动程序支持此值时，WIA 应用程序客户端可以将 **WIA \_ IPA \_ 深度** 设置为此值，以便在设备上启用自动颜色检测。

当 **wia \_ IPA \_ depth** 属性设置为 wia \_ depth AUTO 时 \_ ，wia 迷你驱动程序必须将同一项的 [**wia \_ IPA \_ DATATYPE**](wia-ipa-datatype.md) 属性更新为 wia \_ 数据 \_ 自动 (如果设备支持自动颜色) ，则必须是受支持的值。 当 **wia \_ IPA \_ DATATYPE** 值 wia \_ DATA \_ auto 受支持时， **wia \_ IPA \_ 深度** 值 wia " \_ 自动" \_ 将不再可选且成为必需值。

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

 

 





