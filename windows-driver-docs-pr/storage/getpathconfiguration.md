---
title: GetPathConfiguration 函数
description: GetPathConfiguration 方法用于检索每个路径的设备信息。
ms.assetid: 1661746f-5a5a-48af-b876-c57f19de4923
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
ms.openlocfilehash: 5d81c1dbbd0dd708699cb1f70f5cc068dd02f3d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354075"
---
# <a name="getpathconfiguration-function"></a>GetPathConfiguration 函数


GetPathConfiguration 方法用于检索每个路径的设备信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetPathConfiguration(
   [in, Description("64-bit Path Identifier"):amended] uint64 PathID,
   [out] uint32                                               EntryCount,
   [out, WmiSizeIs("EntryCount")] SCSI_ADDR                   Address[]
);
```

<a name="parameters"></a>Parameters
----------

*PathID*   
64-位域，指定与设备相关联的路径。

*EntryCount*   
32-位域，指示输出中包含的条目数。

*地址\[\]*   
一个数组，包含任意多个 SCSI\_ADDR 结构按照*EntryCount*参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MPIO\_WMI\_方法 WMI 类。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">MPIOwmi.h （包括 MPIOwmi.h）</td>
</tr>
</tbody>
</table>

 

 





