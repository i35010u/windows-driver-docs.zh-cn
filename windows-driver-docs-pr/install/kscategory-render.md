---
title: KSCATEGORY_RENDER
description: KSCATEGORY_RENDER
ms.assetid: 467e3192-46c4-4ef4-88cf-0a870efc1725
keywords:
- KSCATEGORY_RENDER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_RENDER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b16972d6c10d39e5b7e51f6b76edc2d5066bdf6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366713"
---
# <a name="kscategoryrender"></a>KSCATEGORY_RENDER


KSCATEGORY_RENDER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 呈现批和 MIDI 数据流的功能类别。

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
<td align="left"><p>KSCATEGORY_RENDER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{65E8773E-8F56-11D0-A3B9-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频适配器设备驱动程序注册 KSCATEGORY_RENDER 以指示设备支持 KSCATEGORY_RENDER 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的信息，请参阅 INF 文件*Ac97smpl.inf*随[AC'97 示例驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256075)WDK 中。

有关设备的音频的适配器的接口类的信息，请参阅[音频适配器安装设备接口](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)并[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

 

 





