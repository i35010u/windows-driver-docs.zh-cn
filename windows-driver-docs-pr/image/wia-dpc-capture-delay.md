---
title: WIA\_DPC\_捕获\_延迟
description: WIA\_DPC\_捕获\_延迟属性包含一个值，表示时间延迟，以毫秒为单位，应捕获触发器和实际启动的数据捕获之间插入的量。
ms.assetid: dc633117-88b1-4f09-ae64-160a53f75f73
keywords:
- WIA_DPC_CAPTURE_DELAY 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_CAPTURE_DELAY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bf3a1acbd1a69aeada756c72b010ba39ba2dd7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342023"
---
# <a name="wiadpccapturedelay"></a>WIA\_DPC\_捕获\_延迟


WIA\_DPC\_捕获\_延迟属性包含一个值，表示时间延迟，以毫秒为单位，应捕获触发器和实际启动的数据捕获之间插入的量。

## <span id="ddk_wia_dpc_capture_delay_si"></span><span id="DDK_WIA_DPC_CAPTURE_DELAY_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPC\_捕获\_延迟属性不旨在用于描述一个用于启动的帧之间的时间，如突发或时间失效，捕获多个具有单独的间隔属性 ([**WIA\_DPC\_迸发\_间隔**](wia-dpc-burst-interval.md)并[ **WIA\_DPC\_TIMELAPSE\_间隔**](wia-dpc-timelapse-interval.md)分别)。 在这些情况下，WIA\_DPC\_捕获\_延迟仍可作为初始延迟之前捕获序列中的第一个图像时，独立于帧之间的时间。 对于无 precapture 延迟，此属性应设置为零

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


[**WIA\_DPC\_BURST\_INTERVAL**](wia-dpc-burst-interval.md)

[**WIA\_DPC\_TIMELAPSE\_INTERVAL**](wia-dpc-timelapse-interval.md)

 

 






