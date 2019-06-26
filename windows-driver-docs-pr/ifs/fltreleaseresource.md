---
title: FltReleaseResource 例程
description: FltReleaseResource 例程释放当前线程所拥有的指定的资源。
ms.assetid: 2884c596-77ec-4cba-b6cb-000d96cc6342
keywords:
- FltReleaseResource 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FltReleaseResource
api_location:
- fltmgr.sys
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a203ac43821c62122e35f410b330f8e9b3c6e7ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384575"
---
# <a name="fltreleaseresource-routine"></a>FltReleaseResource 例程


**FltReleaseResource**例程释放当前线程所拥有的指定的资源。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltReleaseResource(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>Parameters
----------

*资源* \[in、 out\]  
指向要释放的资源的不透明 ERESOURCE 结构的指针。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**FltReleaseResource**释放以前通过调用获取的资源[ **FltAcquireResourceExclusive** ](fltacquireresourceexclusive.md)或[ **FltAcquireResourceShared**](fltacquireresourceshared.md)。

**FltReleaseResource**是包装[ **ExReleaseResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite) ，可再次正常内核 APC 传递。

因为**FltReleaseResource**可再次正常内核 APC 交付、 不需要调用[ **KeLeaveCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)或者[ **FsRtlExitFileSystem** ](fsrtlexitfilesystem.md)后调用**FltReleaseResource**。

若要获取资源的独占访问权限，调用[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)。

若要获取共享访问的资源，请调用[ **FltAcquireResourceShared**](fltacquireresourceshared.md)。

若要从系统的资源列表中删除资源，请调用[ **ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)。

若要初始化以供重复使用的资源，请调用[ **ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)。

有关 ERESOURCE 结构的详细信息，请参阅[简介 ERESOURCE 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-eresource-routines)内核体系结构设计指南中。

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
<td align="left"><p>此例程是可在 Microsoft Windows XP SP2 上，Microsoft Windows Server 2003 SP1 及更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">FltMgr.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Fltmgr.sys</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)

 

 






