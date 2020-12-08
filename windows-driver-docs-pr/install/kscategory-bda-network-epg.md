---
title: KSCATEGORY_BDA_NETWORK_EPG
description: KSCATEGORY_BDA_NETWORK_EPG
keywords:
- KSCATEGORY_BDA_NETWORK_EPG 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_EPG
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 53b3cd486124e949199f67dbb24a52f988fb4d16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815319"
---
# <a name="kscategory_bda_network_epg"></a>KSCATEGORY_BDA_NETWORK_EPG


KSCATEGORY_BDA_NETWORK_EPG[设备接口类](./overview-of-device-interface-classes.md)是在[广播驱动程序体系结构](/windows-hardware/drivers/ddi/_stream/index)) BDA (中的电子节目指南 (EPG) 的 "[核心流式处理](../stream/streaming-minidrivers2.md) (KS) 功能" 类别中定义的。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_EPG</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{71985F49-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用于 BDA 设备的驱动程序将注册 KSCATEGORY_BDA_NETWORK_EPG 的实例，以指示操作系统设备支持的是 BDA EPG 筛选器。

有关详细信息，请参阅 [BDA 筛选器类别 guid](../stream/bda-filter-category-guids.md)。

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
<td align="left"><p>在 Windows XP 中提供，在 windows 2000 中提供，并在 windows 中安装和更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

 

