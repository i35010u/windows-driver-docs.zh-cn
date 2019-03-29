---
title: WIA\_IPA\_DATATYPE
description: WIA\_IPA\_DATATYPE 属性包含的设备设置的当前数据类型。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: d86c06c2-1d37-4b82-832c-c468c1b4fc33
keywords:
- WIA_IPA_DATATYPE 成像设备
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
ms.openlocfilehash: 0eeb0cb57cc80055d54c3a2a15ea93079aab8a41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566374"
---
# <a name="wiaipadatatype"></a>WIA\_IPA\_DATATYPE


WIA\_IPA\_DATATYPE 属性包含的设备设置的当前数据类型。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_datatype_si"></span><span id="DDK_WIA_IPA_DATATYPE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPA\_DATATYPE 属性来确定图像的数据类型。 应用程序中写入此属性设置要传输的图像的当前数据类型。

下表描述了有效使用 WIA 的常量\_IPA\_数据类型时[ **WIA\_IPA\_格式**](wia-ipa-format.md)未设置属性到 WiaImgFmt\_RAW。

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
<td><p>此值是有效的所有可编程图像数据源项，包括平板和送纸器。 此值的 WIA 微型驱动程序 WIA 应用程序客户端的支持时可以设置：<strong>WIA_IPA_DATATYPE</strong>以便在设备上的自动颜色检测。</p>
<p>当 WIA_DATA_AUTO 设置时，必须更新 WIA 微型驱动程序<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a> WIA_DEPTH_AUTO （它必须是受支持的值，如果设备支持的自动颜色） 到相同的项。</p>
<p>当<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a>支持 WIA_DEPTH_AUTO，值<strong>WIA_IPA_DATATYPE</strong>值 WIA_DATA_AUTO 不再是可选的将成为所需的值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_COLOR</p></td>
<td><p>扫描数据是红-绿-蓝 (RGB)。 通过使用以下 WIA 属性描述了完整的颜色格式：</p>
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
<td><p>相同 WIA_DATA_COLOR，不同之处在于数据通过使用当前所选的抖动模式抖色。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_COLOR_THRESHOLD</p></td>
<td><p>阈值的颜色数据。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_DITHER</p></td>
<td><p>扫描数据通过使用当前所选的抖动模式抖色。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>扫描数据表示强度。 该调色板是固定的等距灰度具有深度的<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a>属性指定。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_THRESHOLD</p></td>
<td><p>阈值是一位每像素的黑白的数据。 对当前值的数据<a href="wia-ips-threshold.md" data-raw-source="[&lt;strong&gt;WIA_IPS_THRESHOLD&lt;/strong&gt;](wia-ips-threshold.md)"> <strong>WIA_IPS_THRESHOLD</strong> </a>转换为白色; 下此值的数据转换为黑色。</p></td>
</tr>
</tbody>
</table>

 

WIA\_IPA\_数据类型属性也用于描述应用程序设置时要使用的原始数据传输的类型[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性值 WiaImgFmt\_RAW。 该驱动程序应设置 WIA\_IPA\_数据类型属性设置为允许该应用程序可以从其选取的值的列表。

下表列出了有效使用 WIA 的常量\_IPA\_数据类型时 WIA\_IPA\_格式设置为 WiaImgFmt\_RAW。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>数据类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>扫描数据表示强度。 该调色板是固定的等距灰度具有深度的<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a>属性指定。</p>
<p><a href="wia-ipa-raw-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_RAW_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-raw-bits-per-channel.md)"> <strong>WIA_IPA_RAW_BITS_PER_CHANNEL</strong> </a>属性必须设置为 1。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_BGR</p></td>
<td><p>扫描数据为 BGR （蓝绿色红） 色彩空间。 通过使用以下 WIA 属性描述了完整的颜色格式：</p>
<ul>
<li><p><a href="wia-ipa-channels-per-pixel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_CHANNELS_PER_PIXEL&lt;/strong&gt;](wia-ipa-channels-per-pixel.md)"><strong>WIA_IPA_CHANNELS_PER_PIXEL</strong></a></p></li>
<li><p><a href="wia-ipa-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-bits-per-channel.md)"><strong>WIA_IPA_BITS_PER_CHANNEL</strong></a></p></li>
<li><p><a href="wia-ipa-pixels-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PIXELS_PER_LINE&lt;/strong&gt;](wia-ipa-pixels-per-line.md)"><strong>WIA_IPA_PIXELS_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-bytes-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BYTES_PER_LINE&lt;/strong&gt;](wia-ipa-bytes-per-line.md)"><strong>WIA_IPA_BYTES_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-number-of-lines.md" data-raw-source="[&lt;strong&gt;WIA_IPA_NUMBER_OF_LINES&lt;/strong&gt;](wia-ipa-number-of-lines.md)"><strong>WIA_IPA_NUMBER_OF_LINES</strong></a></p></li>
</ul>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为 3。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_CMY</p></td>
<td><p>扫描数据位于青色-洋红色-黄色 (CMY) 色彩空间。 通过使用为 WIA_DATA_RAW_BGR 列出的相同 WIA 属性描述了完整的颜色格式。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为 3。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_CMYK</p></td>
<td><p>扫描数据位于青色-洋红色-黄色-黑色 (CMYK) 色彩空间。 通过使用为 WIA_DATA_RAW_BGR 列出的相同 WIA 属性描述了完整的颜色格式。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为 4。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_RGB</p></td>
<td><p>扫描数据位于红-绿-蓝 (RGB) 色彩空间。 使用相同的 WIA 属性如下所示 WIA_DATA_RAW_BGR 描述完整颜色格式。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为 3。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_YUV</p></td>
<td><p>扫描数据为蓝色亮度差异 red 差异 (YUV) 色彩空间。 通过使用为 WIA_DATA_RAW_BGR 列出的相同 WIA 属性描述了完整的颜色格式。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为 3。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_YUVK</p></td>
<td><p>扫描数据为蓝色亮度差异 red 差异-黑色 (YUVK) 色彩空间。 通过使用为 WIA_DATA_RAW_BGR 列出的相同 WIA 属性描述了完整的颜色格式。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL 必须设置为 4。</p></td>
</tr>
</tbody>
</table>

 

如果可以将设备设置一个值，创建 WIA\_PROP\_列表类型并将有效的值放入其中。

检查[ **WIA\_IPA\_深度**](wia-ipa-depth.md)属性来确定位深度。

WIA\_IPA\_数据类型属性通常包含用于相机的单个值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_BITS\_每\_通道**](wia-ipa-bits-per-channel.md)

[**WIA\_IPA\_BYTES\_PER\_LINE**](wia-ipa-bytes-per-line.md)

[**WIA\_IPA\_CHANNELS\_PER\_PIXEL**](wia-ipa-channels-per-pixel.md)

[**WIA\_IPA\_DEPTH**](wia-ipa-depth.md)

[**WIA\_IPA\_格式**](wia-ipa-format.md)

[**WIA\_IPA\_数\_OF\_行**](wia-ipa-number-of-lines.md)

[**WIA\_IPA\_PIXELS\_PER\_LINE**](wia-ipa-pixels-per-line.md)

[**WIA\_IPA\_PLANAR**](wia-ipa-planar.md)

[**WIA\_IPA\_RAW\_BITS\_每\_通道**](wia-ipa-raw-bits-per-channel.md)

[**WIA\_IP\_阈值**](wia-ips-threshold.md)

 

 






