---
title: PKEY\_AudioDevice\_EnableEndpointByDefault
description: PKEY\_AudioDevice\_EnableEndpointByDefault
ms.assetid: bde2c06d-9418-4f6d-960a-0ebec83bf397
ms.date: 01/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 27218a0a235286887158f16e273132fc6b1a6826
ms.sourcegitcommit: 1addd14b2063aba321f5428a23393f22f59c02b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035723"
---
# <a name="pkey_audiodevice_enableendpointbydefault"></a>PKEY\_AudioDevice\_EnableEndpointByDefault

在 windows 7 和更高版本的 Windows 中，终结点生成器将终结点分为外形规格。 这些外形规格基于内核流式处理（KS）筛选器上连接到的终结点的 KSNODETYPE GUID。 当音频终结点生成器枚举某些终结点（例如，其形式因素类型如 UnknownFormFactor）时，终结点生成器会将这些终结点创建为禁用和隐藏状态。 因此，你必须使用控制面板中的声音程序来启用此类终结点，然后才能使用这些终结点。

如果要重写此行为，以便在默认情况下将终结点创建为启用或禁用，Windows 7 将提供**PKEY\_AudioDevice\_EnableEndpointByDefault**注册表项，以便你可以执行此操作。

终结点生成器会创建具有以下任意 KSNODETYPE 值的终结点，并将其禁用并隐藏。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KS 节点类型</th>
<th align="left">外形尺寸</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSCATEGORY_AUDIO</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_BIDIRECTIONAL_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_EMBEDDED_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_EQUALIZATION_NOISE</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_EXTERNAL_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_INPUT_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LEVEL_CALIBRATION_NOISE_SOURCE</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_OUTPUT_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_TELEPHONY_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
</tbody>
</table>

在 windows 7 和更高版本的 Windows 中，外观为 LineLevel 但 KSNODETYPE 不等于 KSNODETYPE\_LINE\_连接器的终结点也创建为禁用和隐藏。 以下终结点属于此类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KS 节点类型</th>
<th align="left">外形尺寸</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODETYPE_1394_DA_STREAM</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_1394_DV_STREAM_SOUNDTRACK</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_TAPE</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_CABLE_TUNER_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_DAT_IO_DIGITAL_AUDIO_TAPE</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_DCC_IO_DIGITAL_COMPACT_CASSETTE</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_DSS_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_DVD_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_MINIDISK</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_MULTITRACK_RECORDER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_PHONOGRAPH</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_RADIO_RECEIVER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_RADIO_TRANSMITTER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SATELLITE_RECEIVER_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_TV_TUNER_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_VCR_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_VIDEO_DISC_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
</tbody>
</table>

以下 INF 文件片段演示了如何使用**PKEY\_AudioDevice\_EnableEndpointByDefault**默认启用或禁用终结点。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,"GLOBAL",USBAudio.Interface
...

[USBAudio.Interface]
AddReg=Xyz.AddReg
...

;; AddReg section to set default behavior of endpoint
[Xyz.AddReg]
HKR,"EP\\n",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_GUID%
HKR,"EP\\n",%PKEY_AudioDevice_EnableEndpointByDefault%,0x00010001,EnableEndpointByDefaultMaskValue
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4"
...
```

在前面的示例中，EnableEndpointByDefaultMaskValue 表示 DWORD 掩码值，它是 "启用" 或 "禁用" 标志（标记\_"启用" 或 "标志"\_"禁用"）和 "数据流" 标志（FLOW\_掩码\_呈现或流\_掩码\_捕获）组合。

以下 INF 文件片段显示了如何设置 CD 播放机，以便在默认情况下启用它并将其配置为输入设备（FLOW\_掩码\_捕获）。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,"GLOBAL",USBAudio.Interface
...

[USBAudio.Interface]
AddReg=MDVAD.EPProperties.AddReg
...

;; AddReg section is used to set default behavior of endpoint for CD player.
;; Enable by default for KSNODETYPE_CD_PLAYER
[MDVAD.EPProperties.AddReg]
HKR,"EP\\0",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_CD_PLAYER%
HKR,"EP\\0",%PKEY_AudioDevice_EnableEndpointByDefault%,0x00010001,0x00000201
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
KSNODETYPE_CD_PLAYER="{DFF220E3-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4"
…
```

在前面的示例中，流\_掩码的按位 "或" 组合\_捕获和标志\_ENABLE 等效于0x00000201 的0x00000200 和0x00000001 的按位 OR 组合。 下表显示了可用于**PKEY\_AudioDevice\_EnableEndpointByDefault**的标志和掩码值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志或终结点掩码</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLAG_DISABLE</p></td>
<td align="left"><p>0x00000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLAG_ENABLE</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLOW_MASK_CAPTURE</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOW_MASK_RENDER</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
</tbody>
</table>
