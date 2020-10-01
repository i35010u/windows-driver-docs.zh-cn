---
title: D3DKMT \_ TDRDBGCTRL \_ 转义结构
description: 了解 D3DKMT \_ TDRDBGCTRL \_ 转义结构，它是为系统使用而保留的。 请勿在您的驱动程序中使用。
ms.assetid: dcb558ed-8072-4454-8aea-d966a65b5d63
keywords:
- D3DKMT_TDRDBGCTRL_ESCAPE 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_TDRDBGCTRL_ESCAPE
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3b7d98fe6a968e7329fee3edce9260f9a9fc29a
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603623"
---
# <a name="d3dkmt_tdrdbgctrl_escape-structure"></a>D3DKMT \_ TDRDBGCTRL \_ 转义结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_TDRDBGCTRL_ESCAPE {
  D3DKMT_TDRDBGCTRLTYPE TdrControl;
  union {
    ULONG NodeOrdinal;
  };
} D3DKMT_TDRDBGCTRL_ESCAPE;
```

<a name="members"></a>成员
-------

**TdrControl**

**NodeOrdinal**

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmthk (包含 D3dkmthk) </td>
</tr>
</tbody>
</table>

 

 





