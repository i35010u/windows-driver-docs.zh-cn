---
title: HS_HOST_FREE_MEMORY 函数
description: HS_HOST_FREE_MEMORY 函数释放以前通过调用 HS_HOST_ALLOCATE_MEMORY 分配的任何内存。
keywords:
- typedef VOID (WINAPI HS_HOST_FREE_MEMORY 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77b07a21ef2ed3705801d9a5c4b350da3a4ee837
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814187"
---
# <a name="hs_host_free_memory-function"></a>HS \_ 主机 \_ 可用 \_ 内存函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**Hs \_ 主机 \_ 可用 \_ 内存** 函数释放先前通过调用 [**HS \_ 主机 \_ 分配 \_ 内存**](hs-host-allocate-memory.md)分配的任何内存。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef VOID (WINAPI *HS_HOST_FREE_MEMORY)(
  _In_     HANDLE hPluginContext,
  _In_opt_ LPVOID pvBuffer
);
```

<a name="parameters"></a>参数
----------

*hPluginContext* \[中\]  
调用此函数的插件的上下文句柄。

*pvBuffer* \[in，可选\]  
指向内存缓冲区的指针。

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

## <a name="see-also"></a>请参阅


[**HS \_ 主机 \_ 分配 \_ 内存**](hs-host-allocate-memory.md)

 

 




