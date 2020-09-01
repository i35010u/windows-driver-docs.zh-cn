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
ms.openlocfilehash: 258621799f184abe08f7b7b78838ba1039648174
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097395"
---
# <a name="kscategory_preferred_waveout_device"></a>KSCATEGORY_PREFERRED_WAVEOUT_DEVICE


为首选波形输入设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_PREFERRED_WAVEIN_DEVICE[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
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

用户在控制面板的多媒体属性页中选择首选的 wave 输入设备。

此功能类别保留供系统提供的 [WDM 音频组件](../audio/wdm-audio-components.md)独占使用。

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
<td align="left"><p>在 windows Server 2003、Windows XP、Windows 2000 及更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

