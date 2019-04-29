---
title: DXGK\_电源\_组件\_P\_标志结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 9A3C9821-7E98-4F9E-94EE-AF2C09C2A881
keywords:
- DXGK_POWER_COMPONENT_P_FLAGS 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_POWER_COMPONENT_P_FLAGS
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03d77419848676876f5f00a4ab32111c659b2084
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350297"
---
# <a name="dxgkpowercomponentpflags-structure"></a>DXGK\_电源\_组件\_P\_标志结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_POWER_COMPONENT_P_FLAGS {
  union {
    struct {
      UINT Reserved  :32;
    };
    UINT Value;
  };
} DXGK_POWER_COMPONENT_P_FLAGS;
```

<a name="members"></a>成员
-------

**保留**

**值**

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
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





