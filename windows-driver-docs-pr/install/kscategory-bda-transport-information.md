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
ms.openlocfilehash: 3f2caf8e9b682e4287c3f8adc135969af8e3b228
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097265"
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

 

