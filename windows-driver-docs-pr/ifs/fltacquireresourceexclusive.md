---
title: FltAcquireResourceExclusive 例程
description: FltAcquireResourceExclusive 例程获取给定资源，以便通过调用线程进行独占访问。
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
ms.openlocfilehash: 34663302454d325037bd1c34cfdea65fca5cf8e9
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852126"
---
# <a name="fltacquireresourceexclusive-routine"></a>FltAcquireResourceExclusive 例程


**FltAcquireResourceExclusive**例程获取给定资源，以便通过调用线程进行独占访问。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltAcquireResourceExclusive(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>参数
----------

*资源* \[in、out\]  
指向不透明的 ERESOURCE 结构的指针。 此结构必须由调用方从非分页池分配，并通过调用[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)或[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)进行初始化。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此例程在 Windows XP Service Pack 2 （SP2）、Windows Server 2003 Service Pack 1 （SP1）和更高版本的 windows 上可用。

**FltAcquireResourceExclusive**通过调用线程获取给定资源以进行独占访问。

以下情况确定是否向调用方授予对给定资源的独占访问权限：

-   如果资源当前不拥有，则立即向当前线程授予独占访问权限。

-   如果调用方已获取了用于独占访问的资源，则会以递归方式向当前线程授予相同的访问类型。

-   对资源具有共享访问权限的调用方必须释放该锁，然后以独占方式重新获取它。

-   如果资源当前由另一个线程作为独占的，或者如果调用方仅具有对资源的共享访问权限，则在获取资源之前，当前线程将进入等待状态。

> [!NOTE]
> 如果两个线程分别持有同一资源上的共享锁，并且这两个线程都尝试单独获取锁定，而不释放其共享锁，它们会死锁。 这意味着，每个线程都将等待另一个线程释放锁定上的共享保留，并且两者都不会释放其共享的保留，直到另一个停止。

 

**FltAcquireResourceExclusive**是用于禁用正常内核 APC 传递的[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)的包装。

因为**FltAcquireResourceExclusive**禁用正常内核 APC 传递，所以在调用**FltAcquireResourceExclusive**之前无需调用[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)或[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md) 。

若要在获取资源后释放资源，请调用[**FltReleaseResource**](fltreleaseresource.md)。 必须通过对**FltReleaseResource**的后续调用来匹配每个对**FltAcquireResourceExclusive**的成功调用。

若要获取共享访问资源，请调用[**FltAcquireResourceShared**](fltacquireresourceshared.md)。

若要从系统资源列表中删除资源，请调用[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)。

若要初始化资源以供重用，请调用[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)。

有关 ERESOURCE 结构的详细信息，请参阅内核体系结构设计指南中的[ERESOURCE 例程简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-eresource-routines)。

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
<td align="left"><p>适用于所有 Windows 操作系统的 Windows XP SP2、Windows Server 2003 SP1 以及更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel （包括 Fltkernel）</td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">FltMgr</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

 

 






