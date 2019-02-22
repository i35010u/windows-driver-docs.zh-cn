---
title: DXGK\_电源\_P\_组件结构
description: 保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 31D76B3B-E939-404B-9EE4-FFCDFCD304C8
keywords:
- DXGK_POWER_P_COMPONENT 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_POWER_P_COMPONENT
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d296e8b9263827c28acc00dbf7992029464a0991
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555648"
---
# <a name="dxgkpowerpcomponent-structure"></a>DXGK\_电源\_P\_组件结构


保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_POWER_P_COMPONENT {
  ULONG                        StateCount;
  DXGK_POWER_P_STATE           States[DXGK_MAX_P_STATES];
  DXGK_POWER_COMPONENT_P_FLAGS Flags;
} DXGK_POWER_P_COMPONENT;
```

<a name="members"></a>成员
-------

**StateCount**

**状态**

**标志**

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





