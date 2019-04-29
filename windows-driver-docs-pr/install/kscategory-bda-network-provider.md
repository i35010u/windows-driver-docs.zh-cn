---
title: KSCATEGORY_BDA_NETWORK_PROVIDER
description: KSCATEGORY_BDA_NETWORK_PROVIDER
ms.assetid: a73f7ea3-19bf-4328-a96f-f28ee91db242
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
ms.openlocfilehash: f3c28d09bcb824d6ddbf2a64e4b234f430a3f2e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377348"
---
# <a name="kscategorybdanetworkprovider"></a>KSCATEGORY_BDA_NETWORK_PROVIDER


KSCATEGORY_BDA_NETWORK_PROVIDER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 中的网络提供程序的功能类别[广播驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff556573)(BDA)。

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

BDA 设备的驱动程序注册 KSCATEGORY_BDA_NETWORK_PROVIDER 向操作系统指示设备支持 BDA 网络提供程序筛选器的实例。

有关详细信息，请参阅[BDA 筛选器类别 Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中可用。 在使用 DirectX 9.0 a 安装 Windows 2000 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

 

 





