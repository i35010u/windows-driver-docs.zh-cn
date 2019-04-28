---
title: WIA\_DPC\_捕获\_模式
description: WIA\_DPC\_捕获\_模式属性设置的映像捕获模式。
ms.assetid: 32d117ac-fa20-49cc-a34e-31a1be88804e
keywords:
- WIA_DPC_CAPTURE_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_CAPTURE_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad79d73dc648069fc20b38e39f9bc09f32f8cb1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342786"
---
# <a name="wiadpccapturemode"></a>WIA\_DPC\_捕获\_模式


WIA\_DPC\_捕获\_模式属性设置的映像捕获模式。

## <span id="ddk_wia_dpc_capture_mode_si"></span><span id="DDK_WIA_DPC_CAPTURE_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的三个常量\_DPC\_捕获\_模式属性。

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
<td><p>CAPTUREMODE_BURST</p></td>
<td><p>捕获的值定义的多个映像中快速连续<a href="wia-dpc-burst-number.md" data-raw-source="[&lt;strong&gt;WIA_DPC_BURST_NUMBER&lt;/strong&gt;](wia-dpc-burst-number.md)"> <strong>WIA_DPC_BURST_NUMBER</strong> </a>并<a href="wia-dpc-burst-interval.md" data-raw-source="[&lt;strong&gt;WIA_DPC_BURST_INTERVAL&lt;/strong&gt;](wia-dpc-burst-interval.md)"> <strong>WIA_DPC_BURST_INTERVAL</strong> </a>属性。</p></td>
</tr>
<tr class="even">
<td><p>CAPTUREMODE_NORMAL</p></td>
<td><p>用于相机的正常模式。</p></td>
</tr>
<tr class="odd">
<td><p>CAPTUREMODE_TIMELAPSE</p></td>
<td><p>定义的捕获多个映像连续<a href="wia-dpc-timelapse-number.md" data-raw-source="[&lt;strong&gt;WIA_DPC_TIMELAPSE_NUMBER&lt;/strong&gt;](wia-dpc-timelapse-number.md)"> <strong>WIA_DPC_TIMELAPSE_NUMBER</strong> </a>并<a href="wia-dpc-timelapse-interval.md" data-raw-source="[&lt;strong&gt;WIA_DPC_TIMELAPSE_INTERVAL&lt;/strong&gt;](wia-dpc-timelapse-interval.md)"> <strong>WIA_DPC_TIMELAPSE_INTERVAL</strong> </a>属性。</p></td>
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

[**WIA\_DPC\_BURST\_NUMBER**](wia-dpc-burst-number.md)

[**WIA\_DPC\_TIMELAPSE\_INTERVAL**](wia-dpc-timelapse-interval.md)

[**WIA\_DPC\_TIMELAPSE\_NUMBER**](wia-dpc-timelapse-number.md)

 

 






