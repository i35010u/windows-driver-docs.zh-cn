---
title: PKEY\_AudioDevice\_EnableEndpointByDefault
description: PKEY\_AudioDevice\_EnableEndpointByDefault
ms.assetid: bde2c06d-9418-4f6d-960a-0ebec83bf397
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35db8b33a882f7a61ddc7046dc1ee1971a0fe769
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332219"
---
# <a name="pkeyaudiodeviceenableendpointbydefault"></a>PKEY\_AudioDevice\_EnableEndpointByDefault


在 Windows 7 和更高版本的 Windows 中，终结点生成器对终结点进行分类为窗体因素。 这些外形规格为基础的流式处理终结点连接到的 (KS) 筛选器的内核上 pin KSNODETYPE GUID。 时音频的终结点生成器枚举特定终结点，例如那些使用 UnknownFormFactor，如外观类型终结点生成器将创建为已禁用或隐藏这些终结点。 因此必须使用声音程序控制面板中启用此类终结点，然后才能使用它们。

如果你想要重写此行为，以便你的终结点创建为启用或禁用默认情况下，Windows 7 提供了**主键\_AudioDevice\_EnableEndpointByDefault**允许您的注册表项若要执行该操作。

终结点生成器为已禁用或隐藏任何以下 KSNODETYPE 值创建终结点。

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

 

在 Windows 7 和更高版本的 Windows 中，终结点具有 LineLevel 外形规格、 但是 KSNODETYPE 不等于 KSNODETYPE\_行\_连接器也创建为已禁用和隐藏。 以下终结点属于此类别。

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

 

下面的 INF 文件片段演示如何使用**主键\_AudioDevice\_EnableEndpointByDefault**启用或禁用终结点，默认情况下。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,”GLOBAL”,USBAudio.Interface
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
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4”
...
```

在前面的示例中，EnableEndpointByDefaultMaskValue 表示 DWORD 掩码值启用或禁用标志的组合 (标志\_启用或标志\_禁用) 和流标志的数据 (流\_掩码\_呈现器或 FLOW\_掩码\_捕获)。

下面的 INF 文件片段演示 CD 播放机的设置方式，以便它默认处于启用状态并被配置为输入设备 (流\_掩码\_捕获)。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,”GLOBAL”,USBAudio.Interface
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
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
KSNODETYPE_CD_PLAYER="{DFF220E3-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4”
…
```

在前面的示例中，流的按位 OR 组合\_掩码\_捕获和标志\_启用相当于按位 OR 组合 0x00000200 和 0x00000001 0x00000201 的结果。 下表显示的标志和可用于的掩码值**主键\_AudioDevice\_EnableEndpointByDefault**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志或终结点的掩码</th>
<th align="left">ReplTest1</th>
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

 

 

 





