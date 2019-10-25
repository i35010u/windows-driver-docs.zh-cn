---
title: FsRtlExitFileSystem 函数
description: FsRtlExitFileSystem 宏会重新启用正常内核模式 Apc，这是由前面对 FsRtlEnterFileSystem 的调用所禁用的。
ms.assetid: 763ceb1c-f614-4268-a7fe-73de0c354c71
keywords:
- FsRtlExitFileSystem 函数可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FsRtlExitFileSystem
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d10444d06d08d273171fa341d40063b34ac35d90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841231"
---
# <a name="fsrtlexitfilesystem-function"></a>FsRtlExitFileSystem 函数


**FsRtlExitFileSystem**宏会重新启用正常内核模式 apc，这是由前面对[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)的调用所禁用的。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FsRtlExitFileSystem(
   VOID 
);
```

<a name="parameters"></a>参数
----------

**   
无

<a name="return-value"></a>返回值
------------

此函数不返回值。

<a name="remarks"></a>备注
-------

每个文件系统驱动程序入口点例程在获取执行文件 i/o 请求所需的资源之前，必须立即调用[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md) ，并立即调用**FsRtlExitFileSystem** 。 这可确保在运行时无法挂起例程，从而阻止其他文件 i/o 请求。

必须通过对**FsRtlExitFileSystem**的后续调用来匹配每个对[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)的成功调用。

请注意，与本地文件系统和网络重定向程序不同的是，文件系统筛选器驱动程序绝不应禁止发送正常内核 Apc （通过调用[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)或[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) ，或提高到 IRQL APC\_级别）调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。

仅当文件系统筛选器驱动程序应禁用正常内核 Apc 时，才会立即调用[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)、 [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)、 [**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)、 [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)或[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)。 调用[**ExReleaseResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)或[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)后，筛选器驱动程序应立即重新启用正常内核 apc 的传送。 作为[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)的替代方法，微筛选器驱动程序可以使用[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [**FltAcquireResourceShared**](fltacquireresourceshared.md)和[**FltReleaseResource**](fltreleaseresource.md)例程，在获取和释放资源。

在调用[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)之前，不需要禁用正常内核 apc，因为此例程调用[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)，这将禁用常规内核和特殊内核 apc。 在调用[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))或[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)之前，还无需执行此操作，因为这些例程禁用正常内核 apc。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))

[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

[**ExReleaseResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)

[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)

 

 






