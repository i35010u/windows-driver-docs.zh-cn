---
title: WIA \_ DPC \_ 焦点 \_ 计量 \_ 模式
description: WIA \_ DPC \_ 焦点 \_ 计量 \_ 模式属性指定相机用来自动调整焦点的模式。
keywords:
- WIA_DPC_FOCUS_METERING_MODE 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FOCUS_METERING_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3184c1dab4f96f1d4966096a7ebf23eeda4be286
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791517"
---
# <a name="wia_dpc_focus_metering_mode"></a>WIA \_ DPC \_ 焦点 \_ 计量 \_ 模式


WIA \_ DPC \_ 焦点 \_ 计量 \_ 模式属性指定相机用来自动调整焦点的模式。

## <span id="ddk_wia_dpc_focus_metering_mode_si"></span><span id="DDK_WIA_DPC_FOCUS_METERING_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表介绍了对 WIA \_ DPC \_ 焦点 \_ 计量 \_ 模式属性有效的常量。

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
<td><p>FOCUSMETERING_CENTERSPOT</p></td>
<td><p>根据中心点调整焦点。</p></td>
</tr>
<tr class="even">
<td><p>FOCUSMETERING_MULTISPOT</p></td>
<td><p>根据 multispot 模式调整焦点。</p></td>
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

 

 





