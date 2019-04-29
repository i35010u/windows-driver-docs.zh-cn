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
ms.openlocfilehash: 71f42b3f9c1b423753d6e21fcd0d33057c696f33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372383"
---
# <a name="kscategoryaudiogfx"></a>KSCATEGORY_AUDIO_GFX


KSCATEGORY_AUDIO_GFX[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 支持的功能类别[全局效果 (GFX) 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff536403)。

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

KS 音频适配器设备驱动程序注册 KSCATEGORY_AUDIO_GFX 向操作系统指示设备支持 KSCATEGORY_AUDIO_GFX 功能分类的实例。

有关音频适配器的其他设备接口类的信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)。

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
<td align="left"><p>在 Windows Server 2003、 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





