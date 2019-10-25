---
title: KSCATEGORY_BDA_NETWORK_EPG
description: KSCATEGORY_BDA_NETWORK_EPG
ms.assetid: 70a02c74-f092-4d1b-bf35-392da5c4fcb6
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
ms.openlocfilehash: 208952b75db421324bd981882ce816195ae91426
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828763"
---
# <a name="kscategory_bda_network_epg"></a>KSCATEGORY_BDA_NETWORK_EPG


KSCATEGORY_BDA_NETWORK_EPG[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)是针对[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)（BDA）中的电子节目指南（EPG）的[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)（KS）功能类别定义的。

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

用于 BDA 设备的驱动程序注册 KSCATEGORY_BDA_NETWORK_EPG 的实例，以向操作系统指明设备支持的是 BDA EPG 筛选器。

有关详细信息，请参阅[BDA 筛选器类别 guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)。

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
<td align="left">Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

 

 





