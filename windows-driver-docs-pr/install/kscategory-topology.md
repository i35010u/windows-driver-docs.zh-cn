---
title: KSCATEGORY_TOPOLOGY
description: KSCATEGORY_TOPOLOGY
ms.assetid: 20c4ccf1-81bb-4209-9842-4de295fe3a00
keywords:
- KSCATEGORY_TOPOLOGY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_TOPOLOGY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15c8ca4c096ac71383e0b68ca59c674700cc8e55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361153"
---
# <a name="kscategorytopology"></a>KSCATEGORY_TOPOLOGY


KSCATEGORY_TOPOLOGY[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)音频设备的内部拓扑 (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_TOPOLOGY</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{DDA54A40-1E4C-11D1-A050-405705C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频适配器设备驱动程序注册 KSCATEGORY_TOPOLOGY 向操作系统指示设备支持 KSCATEGORY_TOPOLOGY 功能分类的实例。

有关设备的音频的适配器的接口类的信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)。

[AC'97 示例驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256075)中提供的 WDK 枚举 KSCATEGORY_TOPOLOGY 设备接口类的实例。

WDK 中的 sysfx 示例注册此设备接口类的实例。 Sysfx 示例位于*src\\音频\\sysfx directory* WDK。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





