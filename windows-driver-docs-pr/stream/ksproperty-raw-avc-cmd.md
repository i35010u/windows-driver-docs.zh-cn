---
title: KSPROPERTY\_RAW\_AVC\_CMD
description: KSPROPERTY\_RAW\_AVC\_CMD 属性发出原始 AV/C 命令。 原始 AV/C 命令仅支持 IEEE 1394 总线的设备。
ms.assetid: f3ff3815-0f4f-4fcb-89bd-e77d8002813c
keywords:
- KSPROPERTY_RAW_AVC_CMD 流式处理媒体设备
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
ms.openlocfilehash: cbf6af0a1b089a5c0432fd1c096fbb320980beb1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382439"
---
# <a name="kspropertyrawavccmd"></a>KSPROPERTY\_RAW\_AVC\_CMD

KSPROPERTY\_RAW\_AVC\_CMD 属性发出原始 AV/C 命令。 原始 AV/C 命令仅支持 IEEE 1394 总线的设备。

## <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>嵌入<strong>RawAVC</strong>结构</p></td>
</tr>
</tbody>
</table>

属性值 （操作数据） 是嵌入**RawAVC** KSPROPERTY 成员\_EXTXPORT\_S 结构描述要运行的原始 AV/C 命令。

## <a name="remarks"></a>备注

此属性仅可以使用与设备可支持 AV/C 命令以及在何处[ **KSPROPERTY\_EXTDEVICE\_端口**](ksproperty-extdevice-port.md)返回适用于开发人员\_端口\_中的 1394年**DevPort**的成员[ **KSPROPERTY\_EXTDEVICE\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)结构。

IEEE 1394 设备驱动程序开发人员还可以选择支持此属性在其驱动程序以扩展设备不支持的标准接口的传输控件 (如用户模式**IAMExtTransport** COM接口方法**放\_模式**并**获取\_模式**)。

不需要 USB 设备上实现支持此属性，因为[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)提供此功能。 应用程序可以使用通常**IKsControl** COM 接口来控制 IEEE 1394 设备。 但是， **IKsControl** COM 接口不提供一种标准方法，以支持磁带查找跨 USB 和 IEEE 1394 总线可移植的。 因此，若要执行磁带查找调用方必须使用**DeviceIoControl**函数而不是**IKsControl** COM 接口。 调用方执行磁带查找 1394年上使用带有绝对原始的 AV/C 命令的 AV/C 设备跟踪数 (ATN) 或代码，以查找到的时间。 这是为什么此属性不适用于 USB 设备的主要原因。

请参阅[数字视频应用程序兼容性](https://go.microsoft.com/fwlink/?linkid=2085071)USB 上的磁带位置搜索和 1394年设备之间的差异的详细信息的白皮书。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)
