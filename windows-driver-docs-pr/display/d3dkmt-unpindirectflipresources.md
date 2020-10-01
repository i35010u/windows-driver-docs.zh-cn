---
title: D3DKMT \_ UNPINDIRECTFLIPRESOURCES 结构
description: 了解 \_ 保留供系统使用的 D3DKMT UNPINDIRECTFLIPRESOURCES 结构。 请勿在您的驱动程序中使用。
ms.assetid: c875a30c-41e4-478c-b8b0-c1fb32672915
keywords:
- D3DKMT_UNPINDIRECTFLIPRESOURCES 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_UNPINDIRECTFLIPRESOURCES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5a07dc46756956a20cdc8594a292744a2b660a04
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603625"
---
# <a name="d3dkmt_unpindirectflipresources-structure"></a>D3DKMT \_ UNPINDIRECTFLIPRESOURCES 结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_UNPINDIRECTFLIPRESOURCES {
  D3DKMT_HANDLE hDevice;
  UINT          ResourceCount;
  D3DKMT_HANDLE *pResourceList;
} D3DKMT_UNPINDIRECTFLIPRESOURCES;
```

<a name="members"></a>成员
-------

**hDevice**

**ResourceCount**

**pResourceList**

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
<td align="left">D3dkmthk (包含 D3dkmthk) </td>
</tr>
</tbody>
</table>

 

 





