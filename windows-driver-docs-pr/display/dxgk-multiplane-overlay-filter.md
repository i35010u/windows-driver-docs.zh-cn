---
title: '\_DXGK\_MULTIPLANE\_覆盖\_筛选器结构'
description: 保留供系统使用。 不要使用它在您的驱动程序中。请注意此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dkmddi.h 标头中可用。 已从更高版本的标头。 .
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
ms.openlocfilehash: 7c242686c494b3d62813b0a6a19ffdfceea760f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350305"
---
# <a name="dxgkmultiplaneoverlayfilter-structure"></a>\_DXGK\_MULTIPLANE\_覆盖\_筛选器结构


保留供系统使用。 不要使用它在您的驱动程序中。

&gt; \[!请注意\]&gt;此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dkmddi.h 标头中可用。 已从更高版本的标头。

 

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
<td align="left">D3dkmddi.h</td>
</tr>
</tbody>
</table>

 

 





