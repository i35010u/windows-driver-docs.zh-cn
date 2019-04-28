---
title: PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint
description: PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint
ms.assetid: cb619972-d9d9-4f33-bb4a-720bfc29e3e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25dcdea96e8c08e213814d6b505b268eccd65864
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332215"
---
# <a name="pkeyaudiodeviceneversetasdefaultendpoint"></a>PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint


您可能会决定设置某些设备，以便永远不会为默认设备被选定。 其中包括，例如，调制解调器线路和医疗音频设备。Windows 7 和更高版本的 Windows 提供了**主键\_AudioDevice\_NeverSetAsDefaultEndpoint**注册表项以允许您阻止设备的终结点的默认终结点作为所选内容。

以下的 INF 文件摘录显示了如何使用**主键\_AudioDevice\_NeverSetAsDefaultEndpoint**来设置终结点，以便它永远不会被选定为默认值。

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

;; AddReg section to setup endpoint so that
;; it cannot be selected as the default endpoint.
[Xyz.AddReg]
HKR,"EP\\n",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_GUID%
HKR,"EP\\n",%PKEY_AudioDevice_NeverSetAsDefaultEndpoint%,0x00010001,NeverSetAsDefaultEndpointMaskValue
...

[Strings]
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
...
```

在前面的示例中，NeverSetAsDefaultEndpointMaskValue 表示是设备角色标志以及数据的流标志的组合的 DWORD 掩码值。

下面的 INF 文件片段演示如何将未定义的输出设备 (KSNODETYPE\_输出\_未定义)，以便在其终结点永远不会选择为默认值，而不考虑设备角色和数据流方向设置。

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

;; AddReg section to setup endpoint so that
;; it cannot be selected as the default endpoint.
[MDVAD.EPProperties.AddReg]
HKR,"EP\\0",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_OUTPUT_UNDEFINED%
HKR,"EP\\0",%PKEY_AudioDevice_NeverSetAsDefaultEndpoint%,0x00010001,0x00000305
...

[Strings]
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
KSNODETYPE_OUTPUT_UNDEFINED="{DFF21CE0-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
```

在上述示例中，0x00000305 是所有标志和适用于掩码的按位 OR 组合**主键\_AudioDevice\_NeverSetAsDefaultEndpoint**。 下表显示了标志和掩码以及其值。

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
<td align="left"><p>FLOW_MASK_CAPTURE</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOW_MASK_RENDER</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ROLE_MASK_COMMUNICATION</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROLE_MASK_CONSOLE</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
</tbody>
</table>

 

 

 





