---
title: WIA \_ DPC \_ 捕获 \_ 延迟
description: "\"WIA \\_ DPC \\_ 捕获 \\_ 延迟\" 属性包含一个值，该值表示在捕获触发器与数据捕获的实际启动之间应插入的时间延迟（以毫秒为单位）。"
keywords:
- WIA_DPC_CAPTURE_DELAY 图像设备
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
ms.openlocfilehash: 4a36d88467d827b9cc6659583e82faac7c707b14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824463"
---
# <a name="wia_dpc_capture_delay"></a>WIA \_ DPC \_ 捕获 \_ 延迟


"WIA \_ DPC \_ 捕获 \_ 延迟" 属性包含一个值，该值表示在捕获触发器与数据捕获的实际启动之间应插入的时间延迟（以毫秒为单位）。

## <span id="ddk_wia_dpc_capture_delay_si"></span><span id="DDK_WIA_DPC_CAPTURE_DELAY_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表或 wia 的 \_ 内容 \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

"WIA \_ dpc \_ 捕获 \_ 延迟" 属性不用于描述单启动、多个捕获（例如突发或时间间隔）的帧之间的时间，它们) 分别 ([**WIA \_ dpc \_ 突发 \_ 间隔**](wia-dpc-burst-interval.md) 和 [**wia \_ dpc \_ TIMELAPSE \_ 时间间隔**](wia-dpc-timelapse-interval.md)。 在这些情况下，WIA \_ DPC \_ 捕获 \_ 延迟仍可用作捕获序列中第一个图像之前的初始延迟，而与帧之间的时间无关。 对于无 precapture 延迟，应将此属性设置为零

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

[**WIA \_ DPC \_ TIMELAPSE \_ 间隔**](wia-dpc-timelapse-interval.md)

 

 






