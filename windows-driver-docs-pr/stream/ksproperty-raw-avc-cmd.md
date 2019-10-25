---
title: KSPROPERTY\_原始\_AVC\_CMD
description: KSPROPERTY\_RAW\_AVC\_CMD 属性发出原始 AV/C 命令。 仅 IEEE 1394 总线设备支持原始 AV/C 命令。
ms.assetid: f3ff3815-0f4f-4fcb-89bd-e77d8002813c
keywords:
- KSPROPERTY_RAW_AVC_CMD 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RAW_AVC_CMD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7beb93bdf99679821789a3502571a6c5b789ef7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838836"
---
# <a name="ksproperty_raw_avc_cmd"></a>KSPROPERTY\_原始\_AVC\_CMD

KSPROPERTY\_RAW\_AVC\_CMD 属性发出原始 AV/C 命令。 仅 IEEE 1394 总线设备支持原始 AV/C 命令。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>Embedded <strong>RawAVC</strong>结构</p></td>
</tr>
</tbody>
</table>

属性值（操作数据）是 KSPROPERTY\_EXTXPORT\_S 结构的嵌入**RawAVC**成员，用于描述要运行的原始 AV/C 命令。

## <a name="remarks"></a>备注

此属性仅可用于可支持 AV/C 命令的设备，以及[**KSPROPERTY\_EXTDEVICE\_端口**](ksproperty-extdevice-port.md)在 KSPROPERTY\_EXTDEVICE 的**DevPort**成员中返回 DEV\_端口\_1394 的设备[ **\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)结构。

适用于 IEEE 1394 设备的驱动程序开发人员可以选择支持其驱动程序中的此属性，以便扩展标准接口不支持的设备传输控件（例如用户模式**IAMExtTransport** COM 接口方法**置于\_模式**并**获取\_模式**）。

不需要在 USB 设备上实现对此属性的支持，因为[Usb 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)提供了此功能。 通常，应用程序可以使用**IKsControl** COM 接口控制 IEEE 1394 设备。 但是， **IKsControl** COM 接口并不提供支持可通过 USB 和 IEEE 1394 总线移植的磁带搜寻的标准方法。 因此，若要执行磁带搜索，调用方必须使用**DeviceIoControl**函数而不是**IKsControl** COM 接口。 调用方通过使用具有绝对跟踪号（ATN）或要搜索的时间代码的原始 AV/C 命令在 1394 AV/C 设备上执行磁带搜寻。 这是此属性不适用于 USB 设备的主要原因。

有关 USB 和1394设备上的磁带位置搜索之间的差异的详细信息，请参阅[数字视频应用程序兼容性](https://go.microsoft.com/fwlink/?linkid=2085071)白皮书。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)
