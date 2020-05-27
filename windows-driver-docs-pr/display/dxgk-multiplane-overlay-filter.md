---
title: '\_DXGK \_ MULTIPLANE \_ 覆盖 \_ 筛选器结构'
description: 预留给系统使用。 不要在您的驱动程序中使用它。请注意，此结构仅在随 Windows 8 随附的 Windows 驱动程序工具包（WDK）版本8随附的 D3dkmddi 标头中可用。 它已从标头的更高版本中删除。.
ms.assetid: db369274-df58-40b0-8f2c-c1963dfa3607
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
ms.openlocfilehash: 93b6148246a304670f97ef5df6886637535a9d91
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851732"
---
# <a name="_dxgk_multiplane_overlay_filter-structure"></a>\_DXGK \_ MULTIPLANE \_ 覆盖 \_ 筛选器结构


预留给系统使用。 不要在您的驱动程序中使用它。

> [!NOTE]
>  此结构仅在随 Windows 8 随附的 Windows 驱动程序工具包（WDK）版本8随附的 D3dkmddi 标头中可用。 它已从标头的更高版本中删除。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_MULITPLANE_OVERLAY_FILTER {
  DXGK_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                Enabled;
  INT                                 Value;
} DXGK_MULTIPLANE_OVERLAY_FILTER;
```

<a name="members"></a>成员
-------

**FilterType**

**Enabled**

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi</td>
</tr>
</tbody>
</table>

 

 





