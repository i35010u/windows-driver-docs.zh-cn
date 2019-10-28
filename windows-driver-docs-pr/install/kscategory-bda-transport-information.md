---
title: KSCATEGORY_BDA_TRANSPORT_INFORMATION
description: KSCATEGORY_BDA_TRANSPORT_INFORMATION
ms.assetid: 0af3159c-8c44-4c42-8141-944bb734623c
keywords:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b9afac2662c6f043bdc6ba1ff605473e8260e38
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837446"
---
# <a name="kscategory_bda_transport_information"></a>KSCATEGORY_BDA_TRANSPORT_INFORMATION


在[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)（BDA）中，为传输信息筛选器（.tif）的[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)（KS）功能类别定义了 KSCATEGORY_BDA_TRANSPORT_INFORMATION[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。

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
<td align="left"><p>KSCATEGORY_BDA_TRANSPORT_INFORMATION</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A2E3074F-6C3D-11d3-B653-00C04F79498E}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

用于 BDA 设备的驱动程序注册 KSCATEGORY_BDA_TRANSPORT_INFORMATION 的实例，以向操作系统指明设备支持的是 BDA 传输信息筛选器。

有关 BDA 传输信息筛选器的 KS 功能类别的详细信息，请参阅[Bda 筛选器类别 guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)。

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

 

 





