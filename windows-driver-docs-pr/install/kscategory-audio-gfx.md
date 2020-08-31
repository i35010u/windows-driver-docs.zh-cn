---
title: KSCATEGORY_AUDIO_GFX
description: KSCATEGORY_AUDIO_GFX
ms.assetid: 6346d7c6-9ea9-450f-af6a-44dec22bf936
keywords:
- KSCATEGORY_AUDIO_GFX 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_AUDIO_GFX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5d9cdfcd6f2f97418315c3790c39e876981369e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095495"
---
# <a name="kscategory_audio_gfx"></a>KSCATEGORY_AUDIO_GFX


KSCATEGORY_AUDIO_GFX [设备接口类](./overview-of-device-interface-classes.md) 是为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的，它支持 [ (GFX) 筛选器的全局效果](../audio/index.md)。

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
<td align="left"><p>KSCATEGORY_AUDIO_GFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{9BAF9572-340C-11D3-ABDC-00A0C90AB16F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 KS 音频适配器设备的驱动程序将 KSCATEGORY_AUDIO_GFX 的实例注册，以指示操作系统设备支持 KSCATEGORY_AUDIO_GFX 功能类别。

有关音频适配器的其他设备接口类的信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)。

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
<td align="left"><p>在 windows Server 2003、Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

