---
title: KSCATEGORY_BDA_RECEIVER_COMPONENT
description: KSCATEGORY_BDA_RECEIVER_COMPONENT
ms.assetid: f160662e-651c-444f-aa82-cfc73c19e41d
keywords:
- KSCATEGORY_BDA_RECEIVER_COMPONENT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_RECEIVER_COMPONENT
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2b22f7b15927046f104498207022a91a8a4874f
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097267"
---
# <a name="kscategory_bda_receiver_component"></a>KSCATEGORY_BDA_RECEIVER_COMPONENT


为[广播驱动程序体系结构](/windows-hardware/drivers/ddi/_stream/index)中的接收[方 (KS](../stream/streaming-minidrivers2.md)) 功能类别定义 KSCATEGORY_BDA_RECEIVER_COMPONENT[设备接口类](./overview-of-device-interface-classes.md) (BDA) 。

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
<td align="left"><p>KSCATEGORY_BDA_RECEIVER_COMPONENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{FD0A5AF4-B41D-11d2-9C95-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用于 BDA 设备的驱动程序将注册 KSCATEGORY_BDA_RECEIVER_COMPONENT 的实例，以向操作系统指明设备支持的是 BDA 接收方筛选器。

有关 BDA 接收方筛选器的 KS 功能类别的详细信息，请参阅 [公共控制节点和筛选器](../stream/common-control-nodes-and-filters.md)， [启动 Bda 微型驱动程序](../stream/starting-a-bda-minidriver.md)和 [bda 筛选器类别 guid](../stream/bda-filter-category-guids.md)。

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

 

