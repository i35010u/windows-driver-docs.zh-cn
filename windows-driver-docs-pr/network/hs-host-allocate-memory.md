---
title: HS_HOST_ALLOCATE_MEMORY 函数
description: HS_HOST_ALLOCATE_MEMORY 函数将返回由调用方指定的内存量。
ms.assetid: afa59680-d85b-4be5-8642-152ff653a0b0
keywords:
- 与 Windows Vista 一起启动的网络驱动程序 (WINAPI HS_HOST_ALLOCATE_MEMORY) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 472bddbe033ffc6a6dd175a9c950c4e4216967f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349677"
---
# <a name="hshostallocatememory-function"></a>HS\_主机\_分配\_内存函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_主机\_分配\_内存**函数返回由调用方指定的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 (WINAPI *HS_HOST_ALLOCATE_MEMORY)(
  _In_  HANDLE                        hPluginContext,
  _In_  DWORD                         dwByteCount,
  _Out_ _bcount (dwByteCount) LPVOID* ppvBuffer
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
此函数在调用插件的上下文句柄。

*dwByteCount* \[in\]  
要分配的内存量。

*ppvBuffer* \[out\]  
指向包含已分配的内存缓冲区的指针。

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
<td><p>Version</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




