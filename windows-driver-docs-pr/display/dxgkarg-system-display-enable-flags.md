---
title: DXGKARG\_系统\_显示\_启用\_标志结构
description: 保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: f23d6692-4c9d-48eb-8d7f-ef70334494b1
keywords:
- DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS 结构显示设备
- PDXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS 结构指针的显示设备
topic_type:
- apiref
api_name:
- DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3fcae06de43c0499f557e3793f0066d41a63328d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384499"
---
# <a name="dxgkargsystemdisplayenableflags-structure"></a>DXGKARG\_系统\_显示\_启用\_标志结构


保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS {
  union {
    struct {
      UINT Reserved  :32;
    };
    UINT   Value;
  };
} DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS, *PDXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS;
```

<a name="members"></a>成员
-------

**保留**保留供系统使用。

**值**保留供系统使用。

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
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h</td>
</tr>
</tbody>
</table>

 

 





