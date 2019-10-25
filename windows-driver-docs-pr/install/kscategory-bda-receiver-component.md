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
ms.openlocfilehash: f3655ca89af5103eff28f8c236481b82bc023662
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828728"
---
# <a name="kscategory_bda_receiver_component"></a>KSCATEGORY_BDA_RECEIVER_COMPONENT


对于[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)（BDA）中接收方的[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)（KS）功能类别，会定义 KSCATEGORY_BDA_RECEIVER_COMPONENT[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。

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

用于 BDA 设备的驱动程序注册 KSCATEGORY_BDA_RECEIVER_COMPONENT 的实例，以向操作系统指明设备支持的是 BDA 接收方筛选器。

有关 BDA 接收方筛选器的 KS 功能类别的详细信息，请参阅[公共控制节点和筛选器](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)，[启动 Bda 微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/starting-a-bda-minidriver)和[bda 筛选器类别 guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)。

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

 

 





