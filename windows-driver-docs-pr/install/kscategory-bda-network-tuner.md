---
title: KSCATEGORY_BDA_NETWORK_TUNER
description: KSCATEGORY_BDA_NETWORK_TUNER
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
ms.openlocfilehash: 8d0df25f3ccb11cca61874c091bd36d1a82cf560
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790563"
---
# <a name="kscategory_bda_network_tuner"></a>KSCATEGORY_BDA_NETWORK_TUNER


为[广播驱动程序体系结构](/windows-hardware/drivers/ddi/_stream/index)中的网络[调谐器 (KS](../stream/streaming-minidrivers2.md)) 功能类别定义 KSCATEGORY_BDA_NETWORK_TUNER[设备接口类](./overview-of-device-interface-classes.md) (BDA) 。

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

用于 BDA 设备的驱动程序将注册 KSCATEGORY_BDA_NETWORK_TUNER 的实例，以指示操作系统设备支持的是 BDA 网络调谐器筛选器。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 INF 文件 *BDASwTunerATSC*。 *BDASwTunerATSC* 包含在 WDK 的 *src \\ swtuner \\ BDATUNER \\ gentuner* 子目录中的 BDA 示例通用调谐器。

有关网络调谐器筛选器的 KS 功能类别的详细信息，请参阅 [公共控制节点和筛选](../stream/common-control-nodes-and-filters.md) 器和 [BDA 筛选器类别 guid](../stream/bda-filter-category-guids.md)。

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

 

