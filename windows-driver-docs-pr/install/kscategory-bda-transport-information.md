---
title: KSCATEGORY_BDA_TRANSPORT_INFORMATION
description: KSCATEGORY_BDA_TRANSPORT_INFORMATION
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
ms.openlocfilehash: 8bd1c57fce6df44636316a192938ccd9d7da9817
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839897"
---
# <a name="kscategory_bda_transport_information"></a>KSCATEGORY_BDA_TRANSPORT_INFORMATION


在[广播驱动程序体系结构) BDA (的广播驱动程序体系结构](/windows-hardware/drivers/ddi/_stream/index)中，为[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能 (类别定义 KSCATEGORY_BDA_TRANSPORT_INFORMATION[设备接口类](./overview-of-device-interface-classes.md)。

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

用于 BDA 设备的驱动程序将注册 KSCATEGORY_BDA_TRANSPORT_INFORMATION 的实例，以向操作系统指明设备支持的是 BDA 传输信息筛选器。

有关 BDA 传输信息筛选器的 KS 功能类别的详细信息，请参阅 [Bda 筛选器类别 guid](../stream/bda-filter-category-guids.md)。

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

 

