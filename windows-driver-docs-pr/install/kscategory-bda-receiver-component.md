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
ms.openlocfilehash: 601fcc7aafa24d14c16a14beeaaeccbc9e94f20f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384260"
---
# <a name="kscategorybdareceivercomponent"></a>KSCATEGORY_BDA_RECEIVER_COMPONENT


KSCATEGORY_BDA_RECEIVER_COMPONENT[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 中为接收方的功能类别[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index) (BDA)。

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

BDA 设备的驱动程序注册 KSCATEGORY_BDA_RECEIVER_COMPONENT 向操作系统指示设备支持 BDA 接收方筛选器的实例。

详细了解 KS 功能类别 BDA 接收方筛选器，请参阅[常见控制节点和筛选器](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)，[启动 BDA 微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/starting-a-bda-minidriver)，和[BDA 筛选器类别 Guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids).

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
<td align="left"><p>在 Windows XP、 DirectX 9.0 a 安装，Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

 

 





