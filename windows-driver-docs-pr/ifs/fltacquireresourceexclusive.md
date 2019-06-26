---
title: FltAcquireResourceExclusive 例程
description: FltAcquireResourceExclusive 例程通过调用线程将获取给定的资源的独占访问权限。
ms.assetid: 3736582e-33eb-4967-acfa-4b9d2b8cd87f
keywords:
- FltAcquireResourceExclusive 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FltAcquireResourceExclusive
api_location:
- fltMgr.lib
- fltMgr.dll
api_type:
- LibDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a5ad45adb6e24db8643026cc3402dc809c545c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384578"
---
# <a name="fltacquireresourceexclusive-routine"></a>FltAcquireResourceExclusive 例程


**FltAcquireResourceExclusive**例程通过调用线程将获取给定的资源的独占访问权限。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltAcquireResourceExclusive(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>Parameters
----------

*资源* \[in、 out\]  
指向一个不透明的 ERESOURCE 结构的指针。 此结构必须由非分页缓冲池从调用方分配并通过调用来初始化[ **ExInitializeResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)或[ **ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite).

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此例程是 Windows XP Service Pack 2 (SP2)、 Windows Server 2003 Service Pack 1 (SP1) 和更高版本的 Windows 上可用。

**FltAcquireResourceExclusive**由调用线程将获取给定的资源的独占访问权限。

在以下情况下确定还是时调用方授予对给定资源的独占访问权限：

-   如果不当前拥有该资源，立即将独占访问权限授予当前线程。

-   如果调用方已获得独占访问的资源，当前线程被授予相同类型的访问权限以递归方式。

-   具有共享资源的访问权限的调用方必须释放锁，然后以独占方式重新获取它。

-   如果该资源当前由另一个线程拥有为独占，或如果调用方仅具有共享资源的访问权限，当前线程会处于等待状态直到可以获取资源。

&gt; \[!请注意\]&gt;如果两个线程对同一资源持有共享的锁并且同时尝试获取锁以独占方式而不释放其共享的锁，它们将死锁。 这意味着每个线程会等待另一个以释放其共享锁，这将释放其共享直到另。

 

**FltAcquireResourceExclusive**是包装[ **ExAcquireResourceExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544351)禁用正常内核 APC 传递。

因为**FltAcquireResourceExclusive**禁用正常内核 APC 传递不需要调用[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)或[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)之前，调用**FltAcquireResourceExclusive**。

若要获取它后会释放该资源，请调用[ **FltReleaseResource**](fltreleaseresource.md)。 每次成功调用**FltAcquireResourceExclusive**的后续调用必须匹配**FltReleaseResource**。

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
<td align="left"><p>在 Windows XP SP2、 Windows Server 2003 SP1 和更高版本的所有 Windows 操作系统中可用。</p></td>
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
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)

 

 






