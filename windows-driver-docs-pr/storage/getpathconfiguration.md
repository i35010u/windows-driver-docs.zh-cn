---
title: GetPathConfiguration 函数
description: GetPathConfiguration 方法用于检索每个路径的设备信息。
keywords:
- GetPathConfiguration 函数存储设备
topic_type:
- apiref
api_name:
- GetPathConfiguration
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f59843a48bfed66853a5acfb6e76df2bb382f179
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835250"
---
# <a name="getpathconfiguration-function"></a>GetPathConfiguration 函数


GetPathConfiguration 方法用于检索每个路径的设备信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetPathConfiguration(
   [in, Description("64-bit Path Identifier"):amended] uint64 PathID,
   [out] uint32                                               EntryCount,
   [out, WmiSizeIs("EntryCount")] SCSI_ADDR                   Address[]
);
```

<a name="parameters"></a>参数
----------

*PathID*   
指定与设备关联的路径的64位域。

*EntryCount*   
表示输出包含的条目数的32位域。

*地址\[\]*   
一个数组，其中包含 EntryCount 参数指定的任意多个 SCSI \_ 地址结构。 *EntryCount*

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MPIO \_ wmi \_ 方法 wmi 类。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">MPIOwmi (包含 MPIOwmi) </td>
</tr>
</tbody>
</table>

 

 





