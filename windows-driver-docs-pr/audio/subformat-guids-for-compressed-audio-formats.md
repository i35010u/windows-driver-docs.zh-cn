---
title: 压缩的音频格式的子格式 GUID
description: 压缩的音频格式的子格式 GUID
ms.assetid: f9595d6c-952c-4266-8eb5-5c8581051d28
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d9bd4029d2cf5a21c3d3a3b6fdad4a484f8a46f
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925626"
---
# <a name="subformat-guids-for-compressed-audio-formats"></a>压缩的音频格式的子格式 GUID


对于 Windows 7，已将新的 subformat Guid 添加到 Ksmedia 头文件中，以支持压缩的音频格式。 Subformat Guid 指示数据格式的特定 Subformat。 这些格式由未压缩音频的使用者电子设备协会（CEA）标准定义。

由于 CEA-861-D 标准，你必须确保 CEA 设备不支持的音频格式不会传输到此类设备。 高清晰多媒体接口（HDMI）和[DisplayPort](https://www.displayport.org/)是 CEA 设备的示例。

对于用户模式访问，将在[WAVEFORMATEXTENSIBLE](https://docs.microsoft.com/windows/win32/api/mmreg/ns-mmreg-waveformatextensible)的**SubFormat**成员和[\_WAVEFORMATEXTENSIBLE IEC61937](https://docs.microsoft.com/windows/win32/coreaudio/representing-formats-for-iec-61937-transmissions)的**FormatExt**成员中指定 guid。 对于音频驱动程序的内核模式访问，将在[**\_KSDATARANGE 音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)结构的**DataRange**成员中指定 guid。

下表列出了可用压缩音频格式的 Guid。

**请注意**   ，并非所有可用格式都支持 Windows 7 HD 音频类驱动程序。 Windows 7 支持的格式在表中以星号（\*）表示。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 类型</th>
<th align="left">SubFormat GUID</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"></td>
<td align="left"><p>请参阅流。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>00000000-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_WAVEFORMATEX</p></td>
<td align="left"><p>IEC 60958 PCM<em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>00000092-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL</p></td>
<td align="left"><p>AC-3</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>00000003-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_MPEG1</p></td>
<td align="left"><p>MPEG-2 （Layer1 & 2）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>00000004-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_MPEG3</p></td>
<td align="left"><p>MPEG-2 （第3层）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>00000005-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_MPEG2</p></td>
<td align="left"><p>MPEG-2 （Multichanel）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>00000006-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_AAC</p></td>
<td align="left"><p>高级音频编码 * （ADTS 中的 MPEG-2/4 AAC）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>00000008-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DTS</p></td>
<td align="left"><p>数字影院声音（DTS）<em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0a</p></td>
<td align="left"><p>0000000a-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS</p></td>
<td align="left"><p>杜比数字 Plus</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0f</p></td>
<td align="left"><p>未使用。</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

下表列出了在高比特率音频示例包中传输的音频格式的 Guid。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 类型</th>
<th align="left">SubFormat GUID</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0b</p></td>
<td align="left"><p>0000000b-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DTS_HD</p></td>
<td align="left"><p>DTS-HD （24位，95KHz）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0c</p></td>
<td align="left"><p>0000000c-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_MLP</p></td>
<td align="left"><p>材料（MLP）<em> -经线无损包装（杜比数字 True HD-24 位 196KHz/高达 18M bps，8通道）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0e</p></td>
<td align="left"><p>00000164-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_WMA_PRO</p></td>
<td align="left"><p>Windows Media 音频（WMA） Pro</em></p></td>
</tr>
</tbody>
</table>

 

下表列出了可以由第三方解决方案实现的压缩音频格式的 Guid。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 类型</th>
<th align="left">SubFormat GUID</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>00000008-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_ATRAC</p></td>
<td align="left"><p>自适应转换音频编码（ATRAC）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>00000009-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_ONE_BIT_AUDIO</p></td>
<td align="left"><p>一位音频</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0d</p></td>
<td align="left"><p>0000000d-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DST</p></td>
<td align="left"><p>直接流传输（DST）</p></td>
</tr>
</tbody>
</table>

 

下面的代码示例演示了音频微型端口驱动程序如何定义并[**初始化\_KSDATARANGE 音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构，以便与具有完全功能杜比数字和解码器的 HDMI 接收器一起使用。 此类型的接收器支持44.1 和 48 KHz 的传输速率。

对于 48 KHz 的采样率，音频微型端口驱动程序使用以下代码来定义和初始化[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构。 此代码显示音频微型端口驱动程序公开的数据范围：

```cpp
//Define and initialize KSDATARANGE_AUDIO structure
// for use with a sample rate of 48 KHz.
KSDATARANGE_AUDIO drDDPlus48;
drDDPlus48.DataRange.FormatSize = sizeof(KSDATARANGE_AUDIO);
drDDPlus48.DataRange.Flags = 0; // Ignored.
drDDPlus48.DataRange.SampleSize = 0; // Ignored.
drDDPlus48.DataRange.Reserved = 0;
drDDPlus48.DataRange.MajorFormat = KSDATAFORMAT_TYPE_AUDIO;
drDDPlus48.DataRange.SubFormat = KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS;
drDDPlus48.DataRange.Specifier = KSDATAFORMAT_SPECIFIER_WAVEFORMATEX;
drDDPlus48.MaximumChannels = 2
drDDPlus48.MinimumBitsPerSample = 16; // All encoded data is transmitted at
drDDPlus48.MaximumBitsPerSample = 16; // 16 bits over IEC 60958.
drDDPlus48.MinimumSampleFrequency = 192000; // 48 KHz * 4.
drDDPlus48.MaximumSampleFrequency = 192000;
```

对于 44.1 KHz 的采样率，音频微型端口驱动程序使用以下代码来定义和初始化[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构：

```cpp
//Define and initialize KSDATARANGE_AUDIO structure
// for use with a sample rate of 41.1 KHz.
KSDATARANGE_AUDIO drDDPlus44;
drDDPlus44.DataRange.FormatSize = sizeof(KSDATARANGE_AUDIO);
drDDPlus44.DataRange.Flags = 0 // Ignored.
drDDPlus44.DataRange.SampleSize = 0 // Ignored.
drDDPlus44.DataRange.Reserved = 0; 
drDDPlus44.DataRange.MajorFormat = KSDATAFORMAT_TYPE_AUDIO;
drDDPlus44.DataRange.SubFormat = KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS;
drDDPlus44.DataRange.Specifier = KSDATAFORMAT_SPECIFIER_WAVEFORMATEX;
drDDPlus44.MaximumChannels = 2
drDDPlus44.MinimumBitsPerSample = 16; // All encoded data is transmitted at
drDDPlus44.MaximumBitsPerSample = 16; // 16 bits over IEC 60958.
drDDPlus44.MinimumSampleFrequency = 176400; // 44.1 KHz * 4
drDDPlus44.MaximumSampleFrequency = 176400;
```

 

 




