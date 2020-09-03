---
title: HS_HOST_ALLOCATE_MEMORY 函数
description: HS_HOST_ALLOCATE_MEMORY 函数返回由调用方指定的内存量。
ms.assetid: afa59680-d85b-4be5-8642-152ff653a0b0
keywords:
- 从 Windows Vista 开始 (WINAPI HS_HOST_ALLOCATE_MEMORY) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52eed86ecd74966a5b1575b2c4ebf1f4f35689b5
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403100"
---
# <a name="hs_host_allocate_memory-function"></a>HS \_ 主机 \_ 分配 \_ 内存函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ HOST \_ \_ memory**函数返回由调用方指定的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 (WINAPI *HS_HOST_ALLOCATE_MEMORY)(
  _In_  HANDLE                        hPluginContext,
  _In_  DWORD                         dwByteCount,
  _Out_ _bcount (dwByteCount) LPVOID* ppvBuffer
);
```

<a name="parameters"></a>参数
----------

*hPluginContext* \[中\]  
调用此函数的插件的上下文句柄。

*dwByteCount* \[中\]  
要分配的内存量。

*ppvBuffer* \[弄\]  
指向缓冲区的指针，该缓冲区包含已分配的内存。

<a name="return-value"></a>返回值
------------

此函数由插件调用，以与主机通信并且不返回值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




