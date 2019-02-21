---
title: WIA\_DIP\_HW\_配置
description: WIA\_DIP\_HW\_CONFIG 属性指示的设备使用的连接类型。 WIA 服务创建和维护此属性，并仅 WIA 服务可以对其进行更改。
ms.assetid: c79e9651-120c-4f99-83d2-1920f7fccc73
keywords:
- WIA_DIP_HW_CONFIG 成像设备
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
ms.openlocfilehash: fe776eac82066be5213adfc4a91f9f96715b3b5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543193"
---
# <a name="wiadiphwconfig"></a>WIA\_DIP\_HW\_配置


WIA\_DIP\_HW\_CONFIG 属性指示的设备使用的连接类型。 WIA 服务创建和维护此属性，并仅 WIA 服务可以对其进行更改。

## <span id="ddk_wia_dip_hw_config_si"></span><span id="DDK_WIA_DIP_HW_CONFIG_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DIP\_HW\_配置属性来确定设备的连接类型。

下表介绍可能的值 WIA\_DIP\_HW\_配置。

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
<td><p>并行的设备</p></td>
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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





