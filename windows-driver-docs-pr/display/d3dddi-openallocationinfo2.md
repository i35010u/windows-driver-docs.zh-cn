---
title: D3DDDI\_OPENALLOCATIONINFO2 结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 5C439C23-75B1-422C-850D-6980CC89539B
keywords:
- D3DDDI_OPENALLOCATIONINFO2 结构显示设备
topic_type:
- apiref
api_name:
- D3DDDI_OPENALLOCATIONINFO2
api_location:
- D3dukmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62709710baab35ac23cd373343db9b95f27a7003
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382960"
---
# <a name="d3dddiopenallocationinfo2-structure"></a>D3DDDI\_OPENALLOCATIONINFO2 结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DDDI_OPENALLOCATIONINFO2 {
  D3DKMT_HANDLE          hAllocation;
  const VOID             *pPrivateDriverData;
  UINT                   PrivateDriverDataSize;
  D3DGPU_VIRTUAL_ADDRESS GpuVirtualAddress;
  ULONG_PTR              Reserved[6];
} D3DDDI_OPENALLOCATIONINFO2;
```

<a name="members"></a>成员
-------

**hAllocation**

**pPrivateDriverData**

**PrivateDriverDataSize**

**GpuVirtualAddress**

**保留**

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dukmdt.h （包括 D3dukmdt.h 或 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





