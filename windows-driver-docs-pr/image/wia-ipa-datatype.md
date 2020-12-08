---
title: WIA \_ IPA \_ 数据类型
description: WIA \_ IPA \_ DATATYPE 属性包含设备的当前数据类型设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_DATATYPE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_DATATYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4532e22cac6b1b9e05c07f11e3e5e791e265592
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815391"
---
# <a name="wia_ipa_datatype"></a>WIA \_ IPA \_ 数据类型


WIA \_ IPA \_ DATATYPE 属性包含设备的当前数据类型设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_datatype_si"></span><span id="DDK_WIA_IPA_DATATYPE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ IPA \_ DATATYPE 属性以确定图像的数据类型。 应用程序将写入此属性，以设置即将传输的图像的当前数据类型。

下表介绍 \_ \_ 当 [**wia \_ IPA \_ FORMAT**](wia-ipa-format.md) 属性未设置为 WiaImgFmt RAW 时，对 wia IPA 数据类型有效的常量 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>数据类型</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_AUTO</p></td>
<td><p>此值对所有可编程的图像数据源项（包括平板和送纸器）有效。 如果 WIA 迷你驱动程序支持此值，WIA 应用程序客户端可以将其设置为： <strong>WIA_IPA_DATATYPE</strong> 以便在设备上启用自动颜色检测。</p>
<p>设置 WIA_DATA_AUTO 后，WIA 迷你驱动程序必须将同一项的 <a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"><strong>WIA_IPA_DEPTH</strong></a> 更新为 WIA_DEPTH_AUTO (如果设备支持自动颜色) ，则必须是受支持的值。</p>
<p>如果支持 <a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"><strong>WIA_IPA_DEPTH</strong></a> 值 WIA_DEPTH_AUTO，则 <strong>WIA_IPA_DATATYPE</strong> 值 WIA_DATA_AUTO 将不再是可选的，而是必需值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_COLOR</p></td>
<td><p>扫描数据为红色 (RGB) 。 完整的颜色格式使用以下 WIA 属性进行描述：</p>
<ul>
<li><p><a href="wia-ipa-channels-per-pixel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_CHANNELS_PER_PIXEL&lt;/strong&gt;](wia-ipa-channels-per-pixel.md)"><strong>WIA_IPA_CHANNELS_PER_PIXEL</strong></a></p></li>
<li><p><a href="wia-ipa-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-bits-per-channel.md)"><strong>WIA_IPA_BITS_PER_CHANNEL</strong></a></p></li>
<li><p><a href="wia-ipa-planar.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PLANAR&lt;/strong&gt;](wia-ipa-planar.md)"><strong>WIA_IPA_PLANAR</strong></a></p></li>
<li><p><a href="wia-ipa-pixels-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PIXELS_PER_LINE&lt;/strong&gt;](wia-ipa-pixels-per-line.md)"><strong>WIA_IPA_PIXELS_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-bytes-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BYTES_PER_LINE&lt;/strong&gt;](wia-ipa-bytes-per-line.md)"><strong>WIA_IPA_BYTES_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-number-of-lines.md" data-raw-source="[&lt;strong&gt;WIA_IPA_NUMBER_OF_LINES&lt;/strong&gt;](wia-ipa-number-of-lines.md)"><strong>WIA_IPA_NUMBER_OF_LINES</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_COLOR_DITHER</p></td>
<td><p>与 WIA_DATA_COLOR 相同，不同之处在于数据使用当前选定的仿色模式进行抖动。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_COLOR_THRESHOLD</p></td>
<td><p>颜色阈值数据。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_DITHER</p></td>
<td><p>通过使用当前选定的仿色模式，扫描数据的抖动。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>扫描数据表示强度。 调色板是一个固定的、均匀间距的灰度，其中 <a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"><strong>WIA_IPA_DEPTH</strong></a> 属性指定的深度。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_THRESHOLD</p></td>
<td><p>阈值为黑白数据的每个像素一位。 <a href="wia-ips-threshold.md" data-raw-source="[&lt;strong&gt;WIA_IPS_THRESHOLD&lt;/strong&gt;](wia-ips-threshold.md)"><strong>WIA_IPS_THRESHOLD</strong></a>的当前值的数据将转换为白色;此值下的数据将转换为黑色。</p></td>
</tr>
</tbody>
</table>

 

WIA \_ IPA \_ DATATYPE 属性还用于描述当应用程序将 [**WIA \_ IPA \_ FORMAT**](wia-ipa-format.md) 属性设置为值 WIAIMGFMT raw 时要使用的原始数据传输类型 \_ 。 驱动程序应将 WIA \_ IPA \_ DATATYPE 属性设置为允许应用程序从中选取的值的列表。

下表列出了 \_ \_ wia \_ IPA \_ 格式设置为 WiaImgFmt RAW 时，与 wia IPA 数据类型有效的常量 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>数据类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>扫描数据表示强度。 调色板是一个固定的、均匀间距的灰度，其中 <a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"><strong>WIA_IPA_DEPTH</strong></a> 属性指定的深度。</p>
<p><a href="wia-ipa-raw-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_RAW_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-raw-bits-per-channel.md)"><strong>WIA_IPA_RAW_BITS_PER_CHANNEL</strong></a>属性必须设置为1。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_BGR</p></td>
<td><p>扫描数据位于 BGR (蓝绿-red) colorspace。 完整的颜色格式使用以下 WIA 属性进行描述：</p>
<ul>
<li><p><a href="wia-ipa-channels-per-pixel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_CHANNELS_PER_PIXEL&lt;/strong&gt;](wia-ipa-channels-per-pixel.md)"><strong>WIA_IPA_CHANNELS_PER_PIXEL</strong></a></p></li>
<li><p><a href="wia-ipa-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-bits-per-channel.md)"><strong>WIA_IPA_BITS_PER_CHANNEL</strong></a></p></li>
<li><p><a href="wia-ipa-pixels-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PIXELS_PER_LINE&lt;/strong&gt;](wia-ipa-pixels-per-line.md)"><strong>WIA_IPA_PIXELS_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-bytes-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BYTES_PER_LINE&lt;/strong&gt;](wia-ipa-bytes-per-line.md)"><strong>WIA_IPA_BYTES_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-number-of-lines.md" data-raw-source="[&lt;strong&gt;WIA_IPA_NUMBER_OF_LINES&lt;/strong&gt;](wia-ipa-number-of-lines.md)"><strong>WIA_IPA_NUMBER_OF_LINES</strong></a></p></li>
</ul>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为3。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_CMY</p></td>
<td><p>扫描数据处于青色-洋红色-黄色 (CMY) colorspace。 完整的颜色格式使用为 WIA_DATA_RAW_BGR 列出的 WIA 属性进行描述。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为3。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_CMYK</p></td>
<td><p>扫描数据处于青色-洋红色-黄色-黑色 (CMYK) colorspace。 完整的颜色格式使用为 WIA_DATA_RAW_BGR 列出的 WIA 属性进行描述。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为4。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_RGB</p></td>
<td><p>扫描数据处于红-绿-蓝 (RGB) colorspace 中。 使用与 WIA_DATA_RAW_BGR 中相同的 WIA 属性说明了完整的颜色格式。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为3。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_YUV</p></td>
<td><p>扫描数据处于亮度-蓝色差异-红色差异 (YUV) colorspace。 完整的颜色格式使用为 WIA_DATA_RAW_BGR 列出的 WIA 属性进行描述。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为3。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_YUVK</p></td>
<td><p>扫描数据处于亮度-蓝色差异-红色差-黑色 (YUVK) colorspace。 完整的颜色格式使用为 WIA_DATA_RAW_BGR 列出的 WIA 属性进行描述。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为4。</p></td>
</tr>
</tbody>
</table>

 

如果可以将设备设置为仅使用单个值，请创建一个 WIA 的 " \_ \_ 类型"，并在其中放置有效值。

检查 [**WIA \_ IPA \_ depth**](wia-ipa-depth.md) 属性以确定位深度。

WIA \_ IPA \_ DATATYPE 属性通常包含照相机的单个值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ \_ \_ 每通道 IPA 位数 \_**](wia-ipa-bits-per-channel.md)

[**WIA \_ IPA \_ 字节 \_ / \_ 行**](wia-ipa-bytes-per-line.md)

[**WIA \_ IPA \_ \_ 每像素通道数 \_**](wia-ipa-channels-per-pixel.md)

[**WIA \_ IPA \_ 深度**](wia-ipa-depth.md)

[**WIA \_ IPA \_ 格式**](wia-ipa-format.md)

[**WIA \_ IPA \_ \_ 行数 \_**](wia-ipa-number-of-lines.md)

[**WIA \_ \_ \_ 每行 IPA 像素 \_**](wia-ipa-pixels-per-line.md)

[**WIA \_ IPA \_ 平面**](wia-ipa-planar.md)

[**WIA \_ IPA \_ \_ \_ 每通道原始 \_ 位数**](wia-ipa-raw-bits-per-channel.md)

[**WIA \_ IP \_ 阈值**](wia-ips-threshold.md)

 

 






