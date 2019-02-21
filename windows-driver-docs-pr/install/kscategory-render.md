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
ms.openlocfilehash: a94957eecdf8be9b6f556f1568389f6fe01a3e79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546880"
---
# <a name="kscategoryrender"></a>KSCATEGORY_RENDER


KSCATEGORY_RENDER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 呈现批和 MIDI 数据流的功能类别。

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

有关设备的音频的适配器的接口类的信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)并[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)。

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
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

 

 





