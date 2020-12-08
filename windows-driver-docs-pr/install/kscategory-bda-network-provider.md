---
title: KSCATEGORY_BDA_NETWORK_PROVIDER
description: KSCATEGORY_BDA_NETWORK_PROVIDER
keywords:
- KSCATEGORY_BDA_NETWORK_PROVIDER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_PROVIDER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 36d0e08c4edde230bd8b93b3c669db085c07d9db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815321"
---
# <a name="kscategory_bda_network_provider"></a>KSCATEGORY_BDA_NETWORK_PROVIDER


KSCATEGORY_BDA_NETWORK_PROVIDER[设备接口类](./overview-of-device-interface-classes.md)是为[广播驱动程序体系结构](/windows-hardware/drivers/ddi/_stream/index)中的网络提供[程序 (KS](../stream/streaming-minidrivers2.md)) 功能类别定义的， (BDA) 。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_PROVIDER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{71985F4B-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用于 BDA 设备的驱动程序将注册 KSCATEGORY_BDA_NETWORK_PROVIDER 的实例，以指示操作系统设备支持的是 BDA 网络提供程序筛选器。

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
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中可用。 在已安装 DirectX 9.0 的 Windows 2000 中提供。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

 

