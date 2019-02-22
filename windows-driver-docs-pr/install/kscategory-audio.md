---
title: KSCATEGORY_AUDIO
description: KSCATEGORY_AUDIO
ms.assetid: 5acdca77-ed90-4f20-bdcc-5f51312c9dd7
keywords:
- KSCATEGORY_AUDIO 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_AUDIO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 711c81d0e78b01ca3198556dbc8f086b66cf6ada
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544212"
---
# <a name="kscategoryaudio"></a>KSCATEGORY_AUDIO


KSCATEGORY_AUDIO[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 音频设备的功能类别。

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
<td align="left"><p>KSCATEGORY_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6994AD04-93EF-11D0-A3CC-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频设备的驱动程序注册此设备接口类，以向操作系统指示设备支持 KSCATEGORY_AUDIO 功能分类的实例。

有关设备的音频的适配器的接口类的信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)。

有关如何在一个 INF 文件中注册此功能的类别的信息，请参阅帮助文件*INFViewer.html*并*ac97smpl.inf*，其中所含[AC'97 示例驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256075) WDK 中。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





