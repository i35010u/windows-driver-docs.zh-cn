---
title: KSCATEGORY_PREFERRED_MIDIOUT_DEVICE
description: KSCATEGORY_PREFERRED_MIDIOUT_DEVICE
ms.assetid: b3d93d21-d4f8-4f00-9947-034790f3f7b1
keywords:
- KSCATEGORY_PREFERRED_MIDIOUT_DEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_PREFERRED_MIDIOUT_DEVICE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf5f52954b2c6ab4238743ecda60728b98a5def3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575644"
---
# <a name="kscategorypreferredmidioutdevice"></a>KSCATEGORY_PREFERRED_MIDIOUT_DEVICE


KSCATEGORY_PREFERRED_MIDIOUT_DEVICE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 功能的类别的首选 MIDI 输出设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_PREFERRED_WAVEOUT_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{D6C50674-72C1-11D2-9755-0000F8004788}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用户在控制面板中的多媒体属性页中选择首选的 MIDI 输出设备。

此功能的类别保留供独占使用的系统提供[WDM 音频组件](https://msdn.microsoft.com/library/windows/hardware/ff538905)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Server 2003、 Windows XP、 Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





