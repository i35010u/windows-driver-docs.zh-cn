---
title: CcUnmapFileOffsetFromSystemCache 例程
description: CcUnmapFileOffsetFromSystemCache 例程从系统缓存中删除部分缓存文件。
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
ms.openlocfilehash: c0adc57baf61986c2d932e22b4fb8a55a77d8a96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786847"
---
# <a name="ccunmapfileoffsetfromsystemcache-routine"></a>CcUnmapFileOffsetFromSystemCache 例程


[**CcUnmapFileOffsetFromSystemCache**](ccsetreadaheadgranularityex.md)例程从系统缓存中删除部分缓存文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcUnmapFileOffsetFromSystemCache(
  _In_ PFILE_OBJECT   FileObject,
  _In_ PLARGE_INTEGER FileOffset,
  _In_ ULONG          Length,
  _In_ ULONG          Flags
);
```

<a name="parameters"></a>参数
----------

*FileObject* \[中\]  
指向缓存文件的文件对象的指针，其缓存内存将被取消映射。

*FileOffset* \[中\]  
指向要开始从系统缓存取消映射的文件位置的指针。

*长度* \[中\]  
要从缓存取消映射的文件部分的长度。 如果 *Length* 为0，则文件的内存部分的剩余部分（从 *FileOffset* 开始）将取消映射。

*标志* \[中\]  
未使用。 将 *标志* 设置为0。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

如果将 *FileOffset* 和 *Length* 都设置为0，则会导致 [**CcUnmapFileOffsetFromSystemCache**](ccsetreadaheadgranularityex.md) 取消映射缓存文件的整个内存部分。

当系统缓存中包含大量文件部分时， [**CcUnmapFileOffsetFromSystemCache**](ccsetreadaheadgranularityex.md)允许文件系统驱动程序降低缓存利用率。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

 

 





