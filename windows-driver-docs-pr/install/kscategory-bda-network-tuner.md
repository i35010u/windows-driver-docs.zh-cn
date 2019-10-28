---
title: KSCATEGORY_BDA_NETWORK_TUNER
description: KSCATEGORY_BDA_NETWORK_TUNER
ms.assetid: d3f9d393-c8a1-4280-8796-a1de755f9508
keywords:
- KSCATEGORY_BDA_NETWORK_TUNER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_TUNER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 117cd1684637f8c5d299aafe64c2f3a890c90a85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837453"
---
# <a name="kscategory_bda_network_tuner"></a>KSCATEGORY_BDA_NETWORK_TUNER


KSCATEGORY_BDA_NETWORK_TUNER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)是为[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)（BDA）中的网络调谐器的[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)（KS）功能类别定义的。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_TUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{71985F48-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用于 BDA 设备的驱动程序注册 KSCATEGORY_BDA_NETWORK_TUNER 的实例，以向操作系统指明设备支持的是 BDA 网络调谐器筛选器。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 INF 文件*BDASwTunerATSC*。 *BDASwTunerATSC*包含在*swtuner 中\\\\BDAtuner\\gentuner*子目录的源中的 BDA 示例通用调谐器。

有关网络调谐器筛选器的 KS 功能类别的详细信息，请参阅[公共控制节点和筛选](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)器和[BDA 筛选器类别 guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)。

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

 

 





