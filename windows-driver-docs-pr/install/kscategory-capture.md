---
title: KSCATEGORY_CAPTURE
description: KSCATEGORY_CAPTURE
ms.assetid: b33e9a04-00f2-4cfa-911e-55461ce5aae7
keywords:
- KSCATEGORY_CAPTURE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_CAPTURE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0fe40612ad4d3b9092f3185287fa4bdb70fbdaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377324"
---
# <a name="kscategorycapture"></a>KSCATEGORY_CAPTURE


KSCATEGORY_CAPTURE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 捕获批或 MIDI 数据流的功能类别。

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
<td align="left"><p>KSCATEGORY_CAPTURE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{65E8773D-8F56-11D0-A3B9-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_CAPTURE 以指示设备支持 KSCATEGORY_CAPTURE 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的信息，请参阅*Ac97smpl.inf*附带的 INF 文件[AC'97 示例驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256075)WDK 中提供的。

有关设备的音频的适配器的接口类的信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)。

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

 

 





