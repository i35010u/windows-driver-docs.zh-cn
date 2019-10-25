---
title: KSCATEGORY_BDA_IP_SINK
description: KSCATEGORY_BDA_IP_SINK
ms.assetid: 7c9627b3-2d6b-471c-9101-0768890bfe10
keywords:
- KSCATEGORY_BDA_IP_SINK 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_IP_SINK
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ab5ac8acc4332f3dc371f4c627a65430744719a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828782"
---
# <a name="kscategory_bda_ip_sink"></a>KSCATEGORY_BDA_IP_SINK


对于[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)（BDA）中的接收器筛选器，为 "[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)（KS）" 功能类别定义 KSCATEGORY_BDA_IP_SINK[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。

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
<td align="left"><p>KSCATEGORY_BDA_IP_SINK</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{71985F4A-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用于 BDA 设备的驱动程序注册 KSCATEGORY_BDA_IP_SINK 的实例，以指示设备支持 BDA IP 接收器筛选器。

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
<td align="left"><p>在 Windows Server 2003、Windows XP、带有 DirectX 9.0 的 windows 2000 和更高版本的 windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

 

 





