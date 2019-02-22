---
title: DXGK\_INTERFACESPECIFICDATA 结构
description: DXGK\_INTERFACESPECIFICDATA 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: dc9ad39c-4439-4e01-9825-fc1df3c3adc0
keywords:
- DXGK_INTERFACESPECIFICDATA 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_INTERFACESPECIFICDATA
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc207b66151d857f8e0f810d440e2247f3f79147
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527107"
---
# <a name="dxgkinterfacespecificdata-structure"></a>DXGK\_INTERFACESPECIFICDATA 结构


DXGK\_INTERFACESPECIFICDATA 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_INTERFACESPECIFICDATA {
  HANDLE                     hAdapter;
  DXGKCB_GETHANDLEDATA       pfnGetHandleDataCb;
  DXGKCB_GETHANDLEPARENT     pfnGetHandleParentCb;
  DXGKCB_ENUMHANDLECHILDREN  pfnEnumHandleChildrenCb;
  DXGKCB_NOTIFY_INTERRUPT    pfnNotifyInterruptCb;
  DXGKCB_NOTIFY_DPC          pfnNotifyDpcCb;
  DXGKCB_QUERYVIDPNINTERFACE pfnQueryVidPnInterfaceCb;
  DXGKCB_GETCAPTUREADDRESS   pfnGetCaptureAddressCb;
} DXGK_INTERFACESPECIFICDATA;
```

<a name="members"></a>成员
-------

**hAdapter**保留供系统使用。

**pfnGetHandleDataCb**保留供系统使用。

**pfnGetHandleParentCb**保留供系统使用。

**pfnEnumHandleChildrenCb**保留供系统使用。

**pfnNotifyInterruptCb**保留供系统使用。

**pfnNotifyDpcCb**保留供系统使用。

**pfnQueryVidPnInterfaceCb**保留供系统使用。

**pfnGetCaptureAddressCb**保留供系统使用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





