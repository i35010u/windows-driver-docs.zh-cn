---
title: KSCATEGORY_AUDIO
description: KSCATEGORY_AUDIO
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
ms.openlocfilehash: ed24161b5a0707bad5d6d81296a325fdd7d501ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831393"
---
# <a name="kscategory_audio"></a>KSCATEGORY_AUDIO


为音频设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_AUDIO[设备接口类](./overview-of-device-interface-classes.md)。

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

适用于 KS 音频设备的驱动程序注册此设备接口类的实例，以指示操作系统设备支持 KSCATEGORY_AUDIO 功能类别。

有关音频适配器的设备接口类的信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)。

有关如何在 INF 文件中注册此功能类别的信息，请参阅帮助文件 *INFViewer.html* 和 *ac97smpl*，这些文件包含在 WDK 中的 [AC ' 97 示例驱动程序](/samples/browse/) 中。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

