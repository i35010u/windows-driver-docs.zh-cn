---
title: WIA \_ DPC \_ FNUMBER
description: WIA \_ DPC \_ FNUMBER 属性对应于镜头的光圈（以100缩放的 f-停止数为单位）。
keywords:
- WIA_DPC_FNUMBER 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FNUMBER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a112c03b1d02f2f568ed9ee7dfd32cf215d53af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837757"
---
# <a name="wia_dpc_fnumber"></a>WIA \_ DPC \_ FNUMBER


WIA \_ DPC \_ FNUMBER 属性对应于镜头的光圈（以100缩放的 f-停止数为单位）。

## <span id="ddk_wia_dpc_fnumber_si"></span><span id="DDK_WIA_DPC_FNUMBER_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

\_ \_ 仅当 [**wia \_ dpc \_ 曝露 \_ 模式**](wia-dpc-exposure-mode.md)属性设置为 "EXPOSUREMODE \_ 手动" 或 "EXPOSUREMODE \_ 口径优先级" 时，wia dpc FNUMBER 属性的设置才有效 \_ 。

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

## <a name="see-also"></a>请参阅


[**WIA \_ DPC \_ 曝光 \_ 模式**](wia-dpc-exposure-mode.md)

 

 






