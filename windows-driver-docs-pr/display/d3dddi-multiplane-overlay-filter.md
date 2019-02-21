---
title: D3DDDI\_MULTIPLANE\_覆盖\_筛选器结构
description: 保留供系统使用。 不要使用它在您的驱动程序中。请注意此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dumddi.h 标头中可用。 已从更高版本的标头。 .
ms.assetid: 56276b78-5550-4d93-8a73-b1183deb54da
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER 结构显示设备
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e166be1415c6b129fedcc5b8165634bbe5133b38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525489"
---
# <a name="d3dddimultiplaneoverlayfilter-structure"></a>D3DDDI\_MULTIPLANE\_覆盖\_筛选器结构


保留供系统使用。 不要使用它在您的驱动程序中。

&gt; \[!请注意\]&gt;此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dumddi.h 标头中可用。 已从更高版本的标头。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DDDI_MULITPLANE_OVERLAY_FILTER {
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                  Enabled;
  INT                                   Value;
} D3DDDI_MULTIPLANE_OVERLAY_FILTER;
```

<a name="members"></a>成员
-------

**FilterType**

**已启用**

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
<td align="left"><p>标头</p></td>
<td align="left">D3dumddi.h</td>
</tr>
</tbody>
</table>

 

 





