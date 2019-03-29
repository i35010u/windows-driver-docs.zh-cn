---
title: D3DKMT\_PINDIRECTFLIPRESOURCES 结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: c5c79876-a9b5-44fa-9545-3995118520d0
keywords:
- D3DKMT_PINDIRECTFLIPRESOURCES 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_PINDIRECTFLIPRESOURCES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 168cfc9304dd97130ff29ab6cd9d75a39e664db7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564995"
---
# <a name="d3dkmtpindirectflipresources-structure"></a>D3DKMT\_PINDIRECTFLIPRESOURCES 结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_PINDIRECTFLIPRESOURCES {
  D3DKMT_HANDLE hDevice;
  UINT          ResourceCount;
  D3DKMT_HANDLE *pResourceList;
} D3DKMT_PINDIRECTFLIPRESOURCES;
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

 

 





