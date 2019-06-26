---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE
description: 焦点模式属性控制的自动、 手动和预设焦点模式的照相机。
ms.assetid: FA014A4B-0CD3-4288-B721-4A73CDD28551
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: a9859c6e4a9a620300c7135a03de455498a11106
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355384"
---
# <a name="kspropertycameracontrolextendedfocusmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE

焦点模式属性控制的自动、 手动和预设焦点模式的照相机。

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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING). **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含一个或多个以下的按位 OR 组合视频处理选项。

| 处理和焦点模式                        | 描述                                                                  |
|--------------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO      | 照相机驱动程序使用其自己的处理逻辑的视频。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_MANUAL    | 照相机的驱动程序使用预设的处理方法或基于温度方法。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK      | 当前的视频处理方法已被锁定。                               |
| KSCAMERA\_EXTENDEDPROP\_焦点\_连续        | 没有要重点设置。                                               |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_宏      | 宏范围重要收敛。                                               |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_正常     | 正常范围内的重要收敛。                                              |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_FULLRANGE  | 完整范围重要收敛。                                                |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_无穷大   | 无限范围重要收敛。                                            |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_HYPERFOCAL | Hyperfocal 范围。                                                            |

**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含当前设置为照相机的视频处理标志。 如果 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动设置可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁。

此属性控制是异步的可取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO**

此标志指示完成事件触发时融合了自动焦点操作。 完成后，而且此标志不是组合使用 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁定可能会发生偏离焦点和照相机驱动程序可能会继续尝试收敛。 如果 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁标志是包含，焦点已锁定到第一个聚合并不会更改直到接收到新的焦点命令。

锁定，而不合并 Auto 模式中，已锁定的控件应被不视为执行任何操作由照相机驱动程序。 在 Auto 模式下的组合中的锁定，已锁定的控件应触发新的聚合。

此标志是互斥的与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册和 KSCAMERA\_EXTENDEDPROP\_焦点\_持续标志。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_MANUAL**

手动指示对此视频处理所提供的特定值。 向驱动程序提供了特定值。

此标志不能结合使用 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO、 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁定或 KSCAMERA\_EXTENDEDPROP\_焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK**

如果没有相应 KSCAMERA 的情况下设置此标志\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动标志照相机驱动程序应尝试锁定当前焦点状态和触发器完成事件一次焦点处于锁定状态。 照相机的驱动程序必须不发生更改的焦点状态，直到收到新的焦点命令。 如果 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动结合使用此标志，照相机驱动程序将集中于自动聚焦和锁定焦点移到该聚合点，然后触发了完成事件。 此标志是必须不能与 KSCAMERA 组合\_EXTENDEDPROP\_焦点\_CONTINUOUS 或 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手动。

此标志不能在指定焦点控件的范围标志除非它结合了 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动。 在这种情况下，使用范围标志以确定尝试自动聚焦扫描的位置执行焦点。 然后，在收敛时焦点设置锁和完成事件触发。

**KSCAMERA\_EXTENDEDPROP\_焦点\_连续**

此标志指示焦点是连续的。 没有焦点控件的单个聚合点在这种情况下。 该驱动程序必须接受此请求并立即完成的异步操作。

此标志不能结合使用 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO、 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁定或 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手动。

此模式下是必需的所有驱动程序。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_宏**

此标志指示焦点收敛，应执行宏范围。 确切的重要范围取决于驱动程序。 此标志可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 和 KSCAMERA\_EXTENDEDPROP\_焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_正常**

此标志指示应正常范围内执行的焦点收敛。 确切的重要范围取决于驱动程序。 此标志可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 和 KSCAMERA\_EXTENDEDPROP\_焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_FULLRANGE**

此标志指示焦点收敛，应执行完整范围内。 确切的重要范围取决于驱动程序。 此标志可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 和 KSCAMERA\_EXTENDEDPROP\_焦点\_连续。

此模式下是必需的所有驱动程序。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_无穷大**

此标志指示应无限范围内执行的焦点收敛。 确切的重要范围取决于驱动程序。 此标志可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 和 KSCAMERA\_EXTENDEDPROP\_焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_HYPERFOCAL**

此标志指示应 hyperfocal 范围内执行的焦点收敛。 确切的重要范围取决于驱动程序。 此标志可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 和 KSCAMERA\_EXTENDEDPROP\_焦点\_连续。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求，该驱动程序设置的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)到以下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Version</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0XFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>大小</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL | KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE |</p>
<p>（视频处理和焦点模式支持）</p></td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前视频处理和焦点模式。</td>
</tr>
</tbody>
</table>


如果以前不设置了任何焦点范围标志，则该驱动程序设置**标志**到 KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_FULLRANGE 以及 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动 （默认值）。 成员[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构，它遵循[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)根据焦点模式的要求设置。

**VideoProp.Value.ull**值必须包含当前的曝光度设置，当模式为 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动。

### <a name="setting-the-property"></a>将属性设置

设置该属性是，KSPROPERTY\_类型\_集请求**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)将包含要设置的焦点模式。 **VideoProc.Value**的成员[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)必须时忽略**标志**包含 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO、 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁，KSCAMERA\_EXTENDEDPROP\_焦点\_持续标志。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
