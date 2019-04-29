---
title: KSCATEGORY_PREFERRED_WAVEOUT_DEVICE
description: KSCATEGORY_PREFERRED_WAVEOUT_DEVICE
ms.assetid: bba79780-e89c-4b19-98e0-84bfdb5bbf25
keywords:
- KSCATEGORY_PREFERRED_WAVEOUT_DEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_PREFERRED_WAVEOUT_DEVICE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecab1c3254455a415d6a13b52dc3955f9e386107
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372680"
---
# <a name="kscategorypreferredwaveoutdevice"></a>KSCATEGORY_PREFERRED_WAVEOUT_DEVICE


KSCATEGORY_PREFERRED_WAVEIN_DEVICE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 功能的首选的批输入设备类别。

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
<td align="left"><p>{D6C5066E-72C1-11D2-9755-0000F8004788}</p></td>
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
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Server 2003、 Windows XP、 Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





