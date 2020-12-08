---
title: PKEY \_ AudioDevice \_ NeverSetAsDefaultEndpoint
description: PKEY \_ AudioDevice \_ NeverSetAsDefaultEndpoint
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b87aebf83ee7ded44d62b3f2fa8bda0a0355d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800921"
---
# <a name="pkey_audiodevice_neversetasdefaultendpoint"></a>PKEY \_ AudioDevice \_ NeverSetAsDefaultEndpoint


您可以决定设置某些设备，以便永远不能将其选作默认设备。 例如，调制解调器线路和医疗音频设备。Windows 7 和更高版本的 Windows 提供了 **PKEY \_ AudioDevice \_ NeverSetAsDefaultEndpoint** 注册表项，以允许你阻止将设备终结点选作默认终结点。

以下 INF 文件摘录演示了如何使用 **PKEY \_ AudioDevice \_ NeverSetAsDefaultEndpoint** 设置终结点，以便永远不能将其选为默认值。

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

;; AddReg section to setup endpoint so that
;; it cannot be selected as the default endpoint.
[Xyz.AddReg]
HKR,"EP\\n",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_GUID%
HKR,"EP\\n",%PKEY_AudioDevice_NeverSetAsDefaultEndpoint%,0x00010001,NeverSetAsDefaultEndpointMaskValue
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
...
```

在前面的示例中，NeverSetAsDefaultEndpointMaskValue 表示一个 DWORD 掩码值，它是设备角色标志和数据流标志的组合。

以下 INF 文件片段显示了如何设置未定义的输出设备 (未 \_ \_ 定义的) ，以便不将其终结点默认为默认值，而不管设备角色和数据流方向。

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

;; AddReg section to setup endpoint so that
;; it cannot be selected as the default endpoint.
[MDVAD.EPProperties.AddReg]
HKR,"EP\\0",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_OUTPUT_UNDEFINED%
HKR,"EP\\0",%PKEY_AudioDevice_NeverSetAsDefaultEndpoint%,0x00010001,0x00000305
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
KSNODETYPE_OUTPUT_UNDEFINED="{DFF21CE0-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
```

在前面的示例中，0x00000305 是可用于 **PKEY \_ AudioDevice \_ NeverSetAsDefaultEndpoint** 的所有标志和掩码的按位 "或" 组合。 下表显示了标志和掩码及其值。

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

 

 

 





