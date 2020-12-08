---
title: '\_DXGK \_ MULTIPLANE \_ 覆盖 \_ 筛选器结构'
description: 预留给系统使用。 不要在您的驱动程序中使用它。请注意，此结构仅在随 windows 8 随附的 Windows 驱动程序工具包 (WDK) 版本8中提供。 它已从标头的更高版本中删除。 .
keywords:
- _DXGK_MULTIPLANE_OVERLAY_FILTER 结构显示设备
- DXGK_MULTIPLANE_OVERLAY_FILTER 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_MULTIPLANE_OVERLAY_FILTER
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0bab5887986b1bdf21699f964748aaacd96fc344
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809035"
---
# <a name="_dxgk_multiplane_overlay_filter-structure"></a>\_DXGK \_ MULTIPLANE \_ 覆盖 \_ 筛选器结构


预留给系统使用。 不要在您的驱动程序中使用它。

> [!NOTE]
>  此结构仅在随 windows 8) 版本8随附的 Windows 驱动程序工具包 (的 D3dkmddi 标头中提供。 它已从标头的更高版本中删除。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_MULITPLANE_OVERLAY_FILTER {
  DXGK_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                Enabled;
  INT                                 Value;
} DXGK_MULTIPLANE_OVERLAY_FILTER;
```

<a name="members"></a>成员
-------

**FilterType**

**已启用**

值

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
<td align="left">D3dkmddi</td>
</tr>
</tbody>
</table>

 

 





