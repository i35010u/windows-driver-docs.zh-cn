---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE
description: 焦点模式属性控制照相机的 "自动"、"手动" 和 "预设" 焦点模式。
ms.assetid: FA014A4B-0CD3-4288-B721-4A73CDD28551
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE 流媒体设备
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
ms.openlocfilehash: 4fb6fb1eb23baff1c9beace4461ae1f0a3cb015d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843228"
---
# <a name="ksproperty_cameracontrol_extended_focusmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE

焦点模式属性控制照相机的 "自动"、"手动" 和 "预设" 焦点模式。

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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个视频处理选项的按位 "或" 组合。

| 处理和焦点模式                        | 描述                                                                  |
|--------------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动      | 照相机驱动程序使用其自己的视频处理逻辑。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册    | 照相机驱动程序使用预设处理方法或基于温度的方法。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁      | 当前视频处理方法已锁定。                               |
| KSCAMERA\_EXTENDEDPROP\_聚焦\_连续        | 没有聚合焦点集。                                               |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_宏      | 宏范围焦点。                                               |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_正常     | 正常范围焦点焦点。                                              |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_FULLRANGE  | 完全范围焦点。                                                |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_无穷   | 无限范围焦点焦点。                                            |
| KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_HYPERFOCAL | Hyperfocal 范围。                                                            |

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的视频处理标志。 如果 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动设置可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK 结合在一起。

此属性控件是异步的，可取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动**

此标志指示在触发完成事件时自动焦点操作已聚合。 完成后，如果此标志不是与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁组合在一起的，则焦点可能会发生分叉，照相机驱动程序可能会继续尝试聚合。 如果包含了 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁标志，则焦点将锁定到第一个聚合，并且不会更改，直到接收到新的焦点命令。

锁定，如果不结合使用自动模式，照相机驱动程序应将已锁定的控件视为不能操作。 锁定与 Auto 模式结合使用时，已锁定的控件应会触发新的聚合。

此标志与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手动和 KSCAMERA\_EXTENDEDPROP 互斥，\_连续标志。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册**

手动指示对于此视频处理，提供了特定的值。 为驱动程序提供了特定的值。

此标志不得与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK 或 KSCAMERA\_EXTENDEDPROP\_集中\_连续。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁**

如果设置此标志时没有相应的 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动标志，则照相机驱动程序应该锁定当前焦点状态，并在锁定焦点后触发完成事件。 照相机驱动程序不得改变焦点状态，直到接收到新的焦点命令。 如果 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动合并此标志，则照相机驱动程序将汇聚为自动焦点，并将焦点锁定到该聚合点，然后触发完成事件。 此标志不得与 KSCAMERA\_EXTENDEDPROP\_焦点\_连续或 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册结合。

不能将此标志与焦点控件的范围标志一起指定，除非它与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 一起使用。 在这种情况下，将使用范围标志来执行焦点，以确定尝试自动搜索的位置。 然后，在聚合时，焦点设置锁和完成事件将激发。

**KSCAMERA\_EXTENDEDPROP\_聚焦\_连续**

此标志指示焦点是连续的。 在这种情况下，焦点控制没有单个会合点。 驱动程序必须接受此请求并立即完成异步操作。

此标志不得与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK 或 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手动。

所有驱动程序都需要此模式。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_宏**

此标志指示应为宏范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动和 KSCAMERA\_EXTENDEDPROP\_将焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_正常**

此标志指示应为正常范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动和 KSCAMERA\_EXTENDEDPROP\_将焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_FULLRANGE**

此标志指示应为整个范围执行焦点收敛。 确切的焦点范围取决于驱动程序。 此标志可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动和 KSCAMERA\_EXTENDEDPROP\_将焦点\_连续。

所有驱动程序都需要此模式。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_无穷**

此标志指示应为无限范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动和 KSCAMERA\_EXTENDEDPROP\_将焦点\_连续。

**KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_HYPERFOCAL**

此标志指示应为 hyperfocal 范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动和 KSCAMERA\_EXTENDEDPROP\_将焦点\_连续。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求时，驱动程序会将[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE |</p>
<p>（支持视频处理和焦点模式）</p></td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前视频处理和焦点模式。</td>
</tr>
</tbody>
</table>


如果以前未设置焦点范围标志，则驱动程序会将**标志**设置为 KSCAMERA\_EXTENDEDPROP\_焦点\_范围\_FULLRANGE 和 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO （默认值）。 [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构的成员将按照焦点模式的要求设置[ **\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。

当 mode 为 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 时， **u)** 值必须包含当前的曝光设置。

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET 请求， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的焦点模式。 当**Flags**包含 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO，KSCAMERA\_时，必须忽略[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的**VideoProc**成员EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK、KSCAMERA\_EXTENDEDPROP\_将焦点\_连续标志。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
