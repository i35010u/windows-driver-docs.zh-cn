---
title: PKEY \_ AudioDevice \_ EnableEndpointByDefault
description: PKEY \_ AudioDevice \_ EnableEndpointByDefault
ms.date: 01/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: d88c84dd09c7507fbf05e4d7debf451e81c84be5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800923"
---
# <a name="pkey_audiodevice_enableendpointbydefault"></a>PKEY \_ AudioDevice \_ EnableEndpointByDefault

在 windows 7 和更高版本的 Windows 中，终结点生成器将终结点分为外形规格。 这些外形规格基于内核流式传输 (KS) 筛选器连接到的网络上的 pin 的 KSNODETYPE GUID。 当音频终结点生成器枚举某些终结点（例如，其形式因素类型如 UnknownFormFactor）时，终结点生成器会将这些终结点创建为禁用和隐藏状态。 因此，你必须使用控制面板中的声音程序来启用此类终结点，然后才能使用这些终结点。

如果要重写此行为，以便在默认情况下将终结点创建为已启用或已禁用，Windows 7 将提供 **PKEY \_ AudioDevice \_ EnableEndpointByDefault** 注册表项，以允许你执行此操作。

终结点生成器会创建具有以下任意 KSNODETYPE 值的终结点，并将其禁用并隐藏。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KS 节点类型</th>
<th align="left">外形规格</th>
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

在 windows 7 和更高版本的 Windows 中，外观为 LineLevel 但 KSNODETYPE 不等于 KSNODETYPE 线条连接器的终结点 \_ \_ 也创建为禁用和隐藏。 以下终结点属于此类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KS 节点类型</th>
<th align="left">外形规格</th>
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

以下 INF 文件片段演示了如何使用 **PKEY \_ AudioDevice \_ EnableEndpointByDefault** 默认启用或禁用终结点。

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

在前面的示例中，EnableEndpointByDefaultMaskValue 表示 DWORD 掩码值，它是 "启用" 或 "禁用" 标志的组合 (标志 \_ 启用或标记 \_ 禁用) 并 (流 \_ 掩码 \_ 呈现或流 \_ 屏蔽 \_ 捕获) 。

以下 INF 文件片段显示了如何设置 CD 播放机，以便在默认情况下启用它并将其配置为输入设备 (FLOW \_ 掩码 \_ 捕获) 。

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

在前面的示例中，流掩码捕获和标记 ENABLE 的按位 "或" 组合 \_ \_ 等效于 \_ 0x00000200 和0x00000001 的按位 "或" 组合与 "0x00000201" 的结果。 下表显示了可以与 **PKEY \_ AudioDevice \_ EnableEndpointByDefault** 一起使用的标志和掩码值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志或终结点掩码</th>
<th align="left">“值”</th>
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
