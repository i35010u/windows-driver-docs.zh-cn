---
title: D3DDDI \_ OPENALLOCATIONINFO2 结构
description: 了解 \_ 保留供系统使用的 D3DDDI OPENALLOCATIONINFO2 结构。 请勿在您的驱动程序中使用。
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
ms.openlocfilehash: 5e75ff9da9605875f8cddfac0090098c009f9949
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590373"
---
# <a name="d3dddi_openallocationinfo2-structure"></a>D3DDDI \_ OPENALLOCATIONINFO2 结构


预留给系统使用。 请勿在您的驱动程序中使用。

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

**保护**

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
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dukmdt (包含 D3dukmdt 或 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 





