---
title: DXGKARG \_ 系统 \_ 显示 \_ 启用 \_ 标志结构
description: 了解 DXGKARG \_ 系统 \_ 显示 \_ 启用 \_ 标志结构，该结构保留供系统使用。 不要在您的驱动程序中使用它。
ms.assetid: f23d6692-4c9d-48eb-8d7f-ef70334494b1
keywords:
- DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS 结构显示设备
- PDXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS 结构指针显示设备
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
ms.openlocfilehash: 0903217ee3a269c738ab0ec44b128d56e561ecf8
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603691"
---
# <a name="dxgkarg_system_display_enable_flags-structure"></a>DXGKARG \_ 系统 \_ 显示 \_ 启用 \_ 标志结构


预留给系统使用。 不要在您的驱动程序中使用它。

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

**保留** 保留供系统使用。

**值** 保留供系统使用。

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
<td align="left">Dispmprt</td>
</tr>
</tbody>
</table>

 

 





