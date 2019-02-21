---
title: KSCATEGORY_PREFERRED_WAVEIN_DEVICE
description: KSCATEGORY_PREFERRED_WAVEIN_DEVICE
ms.assetid: d5f20f18-396a-4cb7-b653-038310ce8e42
keywords:
- KSCATEGORY_PREFERRED_WAVEIN_DEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_PREFERRED_WAVEIN_DEVICE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d27182bb6bb4bf463046235084dd38a0f22428e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521733"
---
# <a name="kscategorypreferredwaveindevice"></a>KSCATEGORY_PREFERRED_WAVEIN_DEVICE


KSCATEGORY_PREFERRED_WAVEIN_DEVICE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 功能的首选的批输入设备类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_PREFERRED_WAVEIN_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{D6C50671-72C1-11D2-9755-0000F8004788}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用户在控制面板中的多媒体属性页中选择首选的批输入的设备。

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
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





