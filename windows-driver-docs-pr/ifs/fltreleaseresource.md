---
title: FltReleaseResource 例程
description: FltReleaseResource 例程释放由当前线程拥有的指定资源。
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
ms.openlocfilehash: 44487c5d78bf5bfd2f6ad428a3262258a8e9b227
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826866"
---
# <a name="fltreleaseresource-routine"></a>FltReleaseResource 例程


**FltReleaseResource** 例程释放由当前线程拥有的指定资源。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltReleaseResource(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>参数
----------

*资源* \[in、out\]  
指向要释放的资源的不透明 ERESOURCE 结构的指针。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**FltReleaseResource** 释放以前通过调用 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md) 或 [**FltAcquireResourceShared**](fltacquireresourceshared.md)获取的资源。

**FltReleaseResource** 是 [**ExReleaseResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite) 的包装器，用于会标准内核 APC 交付。

由于 **FltReleaseResource** 会正常内核 APC 传递，因此不需要在调用 **FltReleaseResource** 后调用 [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)或 [**FsRtlExitFileSystem**](fsrtlexitfilesystem.md) 。

若要获取独占访问的资源，请调用 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)。

若要获取共享访问资源，请调用 [**FltAcquireResourceShared**](fltacquireresourceshared.md)。

若要从系统资源列表中删除资源，请调用 [**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)。

若要初始化资源以供重用，请调用 [**ExReinitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)。

有关 ERESOURCE 结构的详细信息，请参阅内核体系结构设计指南中的 [ERESOURCE 例程简介](../kernel/introduction-to-eresource-routines.md) 。

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
<td align="left"><p>此例程在 Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 及更高版本上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">FltMgr</td>
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


[**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**ExReleaseResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)

 

