---
title: CcUnmapFileOffsetFromSystemCache routine
description: CcUnmapFileOffsetFromSystemCache 例程从系统缓存中删除缓存文件的一部分。
ms.assetid: 37C4ACB9-343D-4F5F-A8B8-FB99A7EA274A
keywords:
- CcUnmapFileOffsetFromSystemCache 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- CcUnmapFileOffsetFromSystemCache
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: be3b2fc09ff6a1a808001f191342d724ec9737e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369579"
---
# <a name="ccunmapfileoffsetfromsystemcache-routine"></a>CcUnmapFileOffsetFromSystemCache routine


[ **CcUnmapFileOffsetFromSystemCache** ](ccsetreadaheadgranularityex.md)例程从系统缓存中删除缓存文件的一部分。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcUnmapFileOffsetFromSystemCache(
  _In_ PFILE_OBJECT   FileObject,
  _In_ PLARGE_INTEGER FileOffset,
  _In_ ULONG          Length,
  _In_ ULONG          Flags
);
```

<a name="parameters"></a>Parameters
----------

*FileObject* \[in\]  
指向缓存的缓存内存将被取消映射的文件的文件对象的指针。

*FileOffset* \[in\]  
指向要开始从系统缓存中取消映射的文件位置的指针。

*长度*\[中\]  
要从缓存取消映射的文件的部分的长度。 如果*长度*为 0，则该文件，开始的内存部分的剩余部分*FileOffset*，未映射。

*标志*\[中\]  
不使用。 设置*标志*为 0。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

将两者都设置*FileOffset*并*长度*为 0 将导致[ **CcUnmapFileOffsetFromSystemCache** ](ccsetreadaheadgranularityex.md)取消整个内存部分的映射有关缓存的文件。

[**CcUnmapFileOffsetFromSystemCache** ](ccsetreadaheadgranularityex.md)允许文件系统驱动程序，以减少缓存使用率时系统缓存中包含大量的文件部分。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

 

 





