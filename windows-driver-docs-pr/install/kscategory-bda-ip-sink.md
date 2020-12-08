---
title: KSCATEGORY_BDA_IP_SINK
description: KSCATEGORY_BDA_IP_SINK
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
ms.openlocfilehash: 7e61f8a794a9e94d325a918496143bc2c57e5719
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831391"
---
# <a name="kscategory_bda_ip_sink"></a>KSCATEGORY_BDA_IP_SINK


为[广播驱动程序体系结构](/windows-hardware/drivers/ddi/_stream/index)中的接收器筛选器 (KS) 功能类别[定义了 KSCATEGORY_BDA_IP_SINK](../stream/streaming-minidrivers2.md) [设备接口类](./overview-of-device-interface-classes.md) (BDA) 。

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

用于 BDA 设备的驱动程序将注册 KSCATEGORY_BDA_IP_SINK 的实例，以指示设备支持 BDA IP 接收器筛选器。

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
<td align="left"><p>在 Windows Server 2003、Windows XP、带有 DirectX 9.0 的 windows 2000 和更高版本的 windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

 

