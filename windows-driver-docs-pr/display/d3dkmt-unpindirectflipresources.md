---
title: D3DKMT\_UNPINDIRECTFLIPRESOURCES 结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
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
ms.openlocfilehash: e349daa5992e9e8934c50a55442d6a2714397138
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327155"
---
# <a name="d3dkmtunpindirectflipresources-structure"></a>D3DKMT\_UNPINDIRECTFLIPRESOURCES 结构


保留供系统使用。 不要在您的驱动程序中使用。

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
<td align="left"><p>Header</p></td>
<td align="left">D3dkmthk.h （包括 D3dkmthk.h）</td>
</tr>
</tbody>
</table>

 

 





