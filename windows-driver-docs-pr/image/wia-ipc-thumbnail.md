---
title: WIA \_ IPC \_ 缩略图
description: WIA \_ IPC \_ 缩略图属性包含24位每像素缩略图数据位。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPC_THUMBNAIL 图像设备
topic_type:
- apiref
api_name:
- WIA_IPC_THUMBNAIL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ebb4bb81ce95af5e0bd04be27e742c7fc9f7c63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817193"
---
# <a name="wia_ipc_thumbnail"></a>WIA \_ IPC \_ 缩略图


WIA \_ IPC \_ 缩略图属性包含24位每像素缩略图数据位。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipc_thumbnail_si"></span><span id="DDK_WIA_IPC_THUMBNAIL_SI"></span>


属性类型： VT \_ UI1 |VT \_ 矢量

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA \_ IPC \_ 缩略图属性包含的缩略图数据必须处于未压缩的位图数据，并在32位边界上对齐。 应用程序将读取 " [**wia \_ ipc \_ 缩略图 \_ 宽度**](wia-ipc-thumbnail-width.md) " 和 " [**wia \_ ipc \_ 缩略图 \_ 高度**](wia-ipc-thumbnail-height.md) " 属性的值，并创建一个 BITMAPINFOHEADER 结构 (在 Microsoft Windows SDK 文档) 中进行了介绍。 应用程序应该能够读取 \_ \_ 表示实际缩略图图像数据的 WIA IPC 缩略图属性 () 并使用此属性将数据直接写入新创建的位图以创建缩略图图像。

Wia \_ IPC \_ 缩略图由 wia 微型驱动程序和在 MICROSOFT Windows XP、Windows Me 和更高版本的操作系统上运行的应用程序使用。

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


[**WIA \_ IPC \_ 缩略图 \_ 高度**](wia-ipc-thumbnail-height.md)

[**WIA \_ IPC \_ 缩略图 \_ 宽度**](wia-ipc-thumbnail-width.md)

 

 






