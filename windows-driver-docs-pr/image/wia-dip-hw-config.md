---
title: WIA \_ DIP \_ HW \_ 配置
description: WIA \_ DIP \_ HW \_ CONFIG 属性指明设备使用的连接类型。 WIA 服务创建并维护此属性，并且只有 WIA 服务可以对其进行更改。
keywords:
- WIA_DIP_HW_CONFIG 图像设备
topic_type:
- apiref
api_name:
- WIA_DIP_HW_CONFIG
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaa6fd3aa62531ddc29af24751e89e29065fcc55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824511"
---
# <a name="wia_dip_hw_config"></a>WIA \_ DIP \_ HW \_ 配置


WIA \_ DIP \_ HW \_ CONFIG 属性指明设备使用的连接类型。 WIA 服务创建并维护此属性，并且只有 WIA 服务可以对其进行更改。

## <span id="ddk_wia_dip_hw_config_si"></span><span id="DDK_WIA_DIP_HW_CONFIG_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ DIP \_ HW \_ CONFIG 属性以确定设备的连接类型。

下表描述了 WIA \_ DIP HW CONFIG 的可能 \_ 值 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>通用 WDM 设备</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>SCSI 设备</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>USB 设备</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>串行设备</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>并行设备</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





