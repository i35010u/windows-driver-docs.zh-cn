---
title: FltAcquireResourceShared 例程
description: FltAcquireResourceShared 例程通过调用线程获取用于共享访问的给定资源。
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
ms.openlocfilehash: d3d630a061d2cba4ff08d394a6b06b98a10acc32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841333"
---
# <a name="fltacquireresourceshared-routine"></a>FltAcquireResourceShared 例程


**FltAcquireResourceShared**例程通过调用线程获取用于共享访问的给定资源。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltAcquireResourceShared(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>参数
----------

\[中的*资源*\]  
指向不透明的 ERESOURCE 结构的指针。 此结构必须由调用方从非分页池分配，并通过调用[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)或[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)进行初始化。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此例程在 Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 及更高版本上可用。

**FltAcquireResourceShared**例程通过调用线程获取用于共享访问的给定资源。

是否向调用方授予对给定资源的共享访问权限取决于以下各项：

-   如果资源当前为无所有者，则立即向当前线程授予共享访问权限。

-   如果调用方已获取资源（用于共享或独占访问），则会以递归方式向当前线程授予相同的访问类型。 请注意，进行此调用不会将给定资源的调用方的独占所有权转换为 "共享"。

-   如果资源当前由另一个线程拥有，并且没有线程等待对资源的独占访问，则立即向调用方授予共享访问权限。 如果存在独占等待程序，则调用方进入等待状态。

-   如果资源当前由另一个线程拥有，或者有另一个线程正在等待独占访问，并且调用方没有资源的共享访问权限，则当前线程将进入等待状态，直到可以获取资源。

**FltAcquireResourceShared**是用于禁用正常内核 APC 传递的[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)的包装。

因为**FltAcquireResourceShared**禁用正常内核 APC 传递，所以在调用**FltAcquireResourceShared**之前无需调用[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)或[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md) 。

若要在获取资源后释放资源，请调用[**FltReleaseResource**](fltreleaseresource.md)。 必须通过对**FltReleaseResource**的后续调用来匹配每个对**FltAcquireResourceShared**的成功调用。

若要获取独占访问的资源，请调用[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">全局</a></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel （包括 Fltkernel）</td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">fltMgr</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

 

 






