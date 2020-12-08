---
title: D3DKMT \_ WDDM \_ 2 \_ 0 \_ cap 结构
description: 了解 D3DKMT \_ WDDM \_ 2 \_ 0 \_ cap 结构，它保留供系统使用。 请勿在您的驱动程序中使用。
keywords:
- D3DKMT_WDDM_2_0_CAPS 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_WDDM_2_0_CAPS
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 92468dcd7d2e13e188ffd12d84c1f2ae4cc2376d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841003"
---
# <a name="d3dkmt_wddm_2_0_caps-structure"></a>D3DKMT \_ WDDM \_ 2 \_ 0 \_ cap 结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_WDDM_2_0_CAPS {
  union {
    struct {
      UINT Support64BitAtomics  :1;
      UINT GpuMmuSupported  :1;
      UINT IoMmuSupported  :1;
      UINT Reserved  :29;
    };
    UINT   Value;
  };
} D3DKMT_WDDM_2_0_CAPS;
```

<a name="members"></a>成员
-------

**Support64BitAtomics**

**GpuMmuSupported**

**IoMmuSupported**

Reserved 

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmdt (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 





