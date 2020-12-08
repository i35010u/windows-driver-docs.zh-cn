---
title: WIA \_ DPC \_ 焦点 \_ 模式
description: WIA \_ DPC \_ 焦点 \_ 模式属性定义照相机设备的当前焦点模式设置。
keywords:
- WIA_DPC_FOCUS_MODE 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FOCUS_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: da4337b5517da108db8db8324d9a41acae74dcfa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791511"
---
# <a name="wia_dpc_focus_mode"></a>WIA \_ DPC \_ 焦点 \_ 模式


WIA \_ DPC \_ 焦点 \_ 模式属性定义照相机设备的当前焦点模式设置。

## <span id="ddk_wia_dpc_focus_mode_si"></span><span id="DDK_WIA_DPC_FOCUS_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

设备驱动程序会枚举 WIA \_ DPC \_ FOCUS 模式属性的支持值 \_ ，应用程序将写入此属性以设置照相机设备的焦点模式。

下表描述了对 WIA \_ DPC \_ FOCUS 模式属性有效的常量 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FOCUSMODE_AUTO</p></td>
<td><p>照相机设备配置为自动聚焦。</p></td>
</tr>
<tr class="even">
<td><p>FOCUSMODE_MACROAUTO</p></td>
<td><p>照相机设备配置为使用短范围宏设置自动获得焦点。</p></td>
</tr>
<tr class="odd">
<td><p>FOCUSMODE_MANUAL</p></td>
<td><p>照相机设备被配置为允许用户手动集中精力。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





