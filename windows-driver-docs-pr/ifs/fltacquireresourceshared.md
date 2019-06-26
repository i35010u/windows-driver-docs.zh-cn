---
title: FltAcquireResourceShared 例程
description: FltAcquireResourceShared 例程通过调用线程将获取给定的资源的共享访问。
ms.assetid: 5232cdba-1050-46b6-8c21-177d4cd1721d
keywords:
- FltAcquireResourceShared 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FltAcquireResourceShared
api_location:
- FltMgr.lib
- FltMgr.dll
api_type:
- LibDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c31804be6bd12a9b8a3d2c618c8d9ce3fe67e198
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384580"
---
# <a name="fltacquireresourceshared-routine"></a>FltAcquireResourceShared 例程


**FltAcquireResourceShared**例程通过调用线程将获取给定的资源的共享访问。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltAcquireResourceShared(
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

此例程是可在 Microsoft Windows XP SP2 上，Microsoft Windows Server 2003 SP1 及更高版本。

**FltAcquireResourceShared**例程通过调用线程将获取给定的资源的共享访问。

还是在给定调用方对给定资源的共享的访问取决于以下：

-   如果当前无所有者的资源，则立即将共享访问权限授予当前线程。

-   如果调用方已占用的资源 （共享或独占访问权限），当前线程被授予相同类型的访问权限以递归方式。 请注意，进行此调用不会将转换要共享的给定资源的调用方的独占所有权。

-   如果为当前拥有该资源由另一个线程共享并且没有线程正在等待对资源进行独占访问，立即向调用方授予共享访问权限。 调用方会独占等待应用程序是否处于等待状态。

-   如果该资源当前由另一个线程拥有为独占，或者如果没有另一个线程等待独占访问权限，并且未被调用方不具有共享资源的访问权限，当前线程放置于等待状态，直到可以获取资源。

**FltAcquireResourceShared**是包装[ **ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363)禁用正常内核 APC 传递。

因为**FltAcquireResourceShared**禁用正常内核 APC 传递不需要调用[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)或[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)之前调用**FltAcquireResourceShared**。

若要获取它后会释放该资源，请调用[ **FltReleaseResource**](fltreleaseresource.md)。 每次成功调用**FltAcquireResourceShared**的后续调用必须匹配**FltReleaseResource**。

若要获取资源的独占访问权限，调用[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)。

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
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">FltMgr.lib</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)

 

 






