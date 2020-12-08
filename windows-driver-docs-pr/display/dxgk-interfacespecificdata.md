---
title: DXGK \_ INTERFACESPECIFICDATA 结构
description: DXGK \_ INTERFACESPECIFICDATA 结构保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: c5771147a7734ae5f85fb96fcff15f0b608aced0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809037"
---
# <a name="dxgk_interfacespecificdata-structure"></a>DXGK \_ INTERFACESPECIFICDATA 结构


DXGK \_ INTERFACESPECIFICDATA 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_INTERFACESPECIFICDATA {
  HANDLE                     hAdapter;
  DXGKCB_GETHANDLEDATA       pfnGetHandleDataCb;
  DXGKCB_GETHANDLEPARENT     pfnGetHandleParentCb;
  DXGKCB_ENUMHANDLECHILDREN  pfnEnumHandleChildrenCb;
  DXGKCB_NOTIFY_INTERRUPT    pfnNotifyInterruptCb;
  DXGKCB_NOTIFY_DPC          pfnNotifyDpcCb;
  DXGKCB_QUERYVIDPNINTERFACE pfnQueryVidPnInterfaceCb;
  DXGKCB_GETCAPTUREADDRESS   pfnGetCaptureAddressCb;
} DXGK_INTERFACESPECIFICDATA;
```

<a name="members"></a>成员
-------

**hAdapter** 保留供系统使用。

**pfnGetHandleDataCb** 保留供系统使用。

**pfnGetHandleParentCb** 保留供系统使用。

**pfnEnumHandleChildrenCb** 保留供系统使用。

**pfnNotifyInterruptCb** 保留供系统使用。

**pfnNotifyDpcCb** 保留供系统使用。

**pfnQueryVidPnInterfaceCb** 保留供系统使用。

**pfnGetCaptureAddressCb** 保留供系统使用。

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 





