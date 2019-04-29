---
title: WIA\_IPC\_缩略图
description: WIA\_IPC\_缩略图属性包含的每像素 24 位缩略图的数据位。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 748443a7-cc7f-4291-b987-21462af97c3c
keywords:
- WIA_IPC_THUMBNAIL 成像设备
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
ms.openlocfilehash: 22e04d69180a1924b879a6ed87a0ba2958613274
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378397"
---
# <a name="wiaipcthumbnail"></a>WIA\_IPC\_缩略图


WIA\_IPC\_缩略图属性包含的每像素 24 位缩略图的数据位。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipc_thumbnail_si"></span><span id="DDK_WIA_IPC_THUMBNAIL_SI"></span>


属性类型：VT\_UI1 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

缩略图的数据的 WIA\_IPC\_缩略图属性包含必须处于未压缩的位图数据和 32 位边界上对齐。 应用程序读取的值[ **WIA\_IPC\_缩略图\_宽度**](wia-ipc-thumbnail-width.md)并[ **WIA\_IPC\_缩略图\_高度**](wia-ipc-thumbnail-height.md)属性，并创建一个 BITMAPINFOHEADER 结构 （它 Microsoft Windows SDK 文档中所述）。 应用程序应该能够读取 WIA\_IPC\_缩略图属性 （用于表示实际的缩略图图像数据） 并使用此属性将数据直接写入新创建的位图创建缩略图。

WIA\_IPC\_WIA 微型驱动程序和 Microsoft Windows XP、 Windows Me，和更高版本的操作系统运行的应用程序使用缩略图。

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
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPC\_THUMBNAIL\_HEIGHT**](wia-ipc-thumbnail-height.md)

[**WIA\_IPC\_THUMBNAIL\_WIDTH**](wia-ipc-thumbnail-width.md)

 

 






