---
title: HS_HOST_FREE_MEMORY 函数
description: HS_HOST_FREE_MEMORY 函数释放以前通过 HS_HOST_ALLOCATE_MEMORY 调用已分配任何内存。
ms.assetid: 2090ecf8-e1d5-4410-acbf-1b97f418e185
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef VOID (WINAPI HS_HOST_FREE_MEMORY) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9d9e8a423787f49758a4047adba566420283880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575736"
---
# <a name="hshostfreememory-function"></a>HS\_主机\_免费\_内存函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_主机\_免费\_内存**函数释放以前通过调用已分配任何内存[ **HS\_主机\_分配\_内存**](hs-host-allocate-memory.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef VOID (WINAPI *HS_HOST_FREE_MEMORY)(
  _In_     HANDLE hPluginContext,
  _In_opt_ LPVOID pvBuffer
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
此函数在调用插件的上下文句柄。

*pvBuffer* \[in, optional\]  
指向内存缓冲区的指针。

<a name="return-value"></a>返回值
------------

此函数调用由插件与主机通信，并不会返回一个值。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HS\_主机\_分配\_内存**](hs-host-allocate-memory.md)

 

 




