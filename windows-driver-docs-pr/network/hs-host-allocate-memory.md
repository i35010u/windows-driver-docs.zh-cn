---
title: HS_HOST_ALLOCATE_MEMORY 函数
description: HS_HOST_ALLOCATE_MEMORY 函数返回由调用方指定的内存量。
keywords:
- 从 Windows Vista 开始 (WINAPI HS_HOST_ALLOCATE_MEMORY) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2742e6b55a9dd11c10312127fde38741ca6fe7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814197"
---
# <a name="hs_host_allocate_memory-function"></a>HS \_ 主机 \_ 分配 \_ 内存函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ HOST \_ \_ memory** 函数返回由调用方指定的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 (WINAPI *HS_HOST_ALLOCATE_MEMORY)(
  _In_  HANDLE                        hPluginContext,
  _In_  DWORD                         dwByteCount,
  _Out_ _bcount (dwByteCount) LPVOID* ppvBuffer
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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




