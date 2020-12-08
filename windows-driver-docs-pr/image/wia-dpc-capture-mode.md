---
title: WIA \_ DPC \_ 捕获 \_ 模式
description: WIA \_ DPC \_ 捕获 \_ 模式属性设置映像捕获模式。
keywords:
- WIA_DPC_CAPTURE_MODE 图像设备
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
ms.openlocfilehash: 33224ea03f4c7ff655b6b43e2e307efc7b53d265
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793627"
---
# <a name="wia_dpc_capture_mode"></a>WIA \_ DPC \_ 捕获 \_ 模式


WIA \_ DPC \_ 捕获 \_ 模式属性设置映像捕获模式。

## <span id="ddk_wia_dpc_capture_mode_si"></span><span id="DDK_WIA_DPC_CAPTURE_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了在 WIA \_ DPC \_ 捕获模式属性中有效的三个常量 \_ 。

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
<td><p>按照 " <a href="wia-dpc-burst-number.md" data-raw-source="[&lt;strong&gt;WIA_DPC_BURST_NUMBER&lt;/strong&gt;](wia-dpc-burst-number.md)"><strong>WIA_DPC_BURST_NUMBER</strong></a> " 和 " <a href="wia-dpc-burst-interval.md" data-raw-source="[&lt;strong&gt;WIA_DPC_BURST_INTERVAL&lt;/strong&gt;](wia-dpc-burst-interval.md)"><strong>WIA_DPC_BURST_INTERVAL</strong></a> " 属性的值的定义，快速连续捕获多个映像。</p></td>
</tr>
<tr class="even">
<td><p>CAPTUREMODE_NORMAL</p></td>
<td><p>相机的正常模式。</p></td>
</tr>
<tr class="odd">
<td><p>CAPTUREMODE_TIMELAPSE</p></td>
<td><p>按照 <a href="wia-dpc-timelapse-number.md" data-raw-source="[&lt;strong&gt;WIA_DPC_TIMELAPSE_NUMBER&lt;/strong&gt;](wia-dpc-timelapse-number.md)"><strong>WIA_DPC_TIMELAPSE_NUMBER</strong></a> 和 <a href="wia-dpc-timelapse-interval.md" data-raw-source="[&lt;strong&gt;WIA_DPC_TIMELAPSE_INTERVAL&lt;/strong&gt;](wia-dpc-timelapse-interval.md)"><strong>WIA_DPC_TIMELAPSE_INTERVAL</strong></a> 属性的定义连续捕获多个映像。</p></td>
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

## <a name="see-also"></a>请参阅


[**WIA \_ DPC \_ 突发 \_ 间隔**](wia-dpc-burst-interval.md)

[**WIA \_ DPC \_ 突发 \_ 数量**](wia-dpc-burst-number.md)

[**WIA \_ DPC \_ TIMELAPSE \_ 间隔**](wia-dpc-timelapse-interval.md)

[**WIA \_ DPC \_ TIMELAPSE \_ 号**](wia-dpc-timelapse-number.md)

 

 






