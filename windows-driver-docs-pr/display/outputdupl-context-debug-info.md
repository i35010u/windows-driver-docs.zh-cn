---
title: OUTPUTDUPL \_ 上下文 \_ 调试 \_ 信息结构
description: 了解 OUTPUTDUPL \_ 上下文 \_ 调试 \_ 信息结构，该结构已保留供系统使用。 请勿在您的驱动程序中使用。
keywords:
- OUTPUTDUPL_CONTEXT_DEBUG_INFO 结构显示设备
topic_type:
- apiref
api_name:
- OUTPUTDUPL_CONTEXT_DEBUG_INFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2914bb21267f047e87364a6423bf20c4fdb693d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802619"
---
# <a name="outputdupl_context_debug_info-structure"></a>OUTPUTDUPL \_ 上下文 \_ 调试 \_ 信息结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _OUTPUTDUPL_CONTEXT_DEBUG_INFO {
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS Status;
  HANDLE                          ProcessID;
  UINT32                          AccumulatedPresents;
  LARGE_INTEGER                   LastPresentTime;
  LARGE_INTEGER                   LastMouseTime;
  CHAR                            ProcessName[DXGK_DIAG_PROCESS_NAME_LENGTH];
} OUTPUTDUPL_CONTEXT_DEBUG_INFO;
```

<a name="members"></a>成员
-------

**状态**

**ProcessID**

**AccumulatedPresents**

**LastPresentTime**

**LastMouseTime**

**ProcessName**

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

 

 





