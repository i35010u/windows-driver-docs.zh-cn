---
title: FsRtlExitFileSystem 函数
description: FsRtlExitFileSystem 宏将重新启用 FsRtlEnterFileSystem 前面的调用已禁用的普通的内核模式 Apc 的交付。
ms.assetid: 763ceb1c-f614-4268-a7fe-73de0c354c71
keywords:
- FsRtlExitFileSystem 函数可安装文件系统驱动程序
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
ms.openlocfilehash: 6363505d37a72ddd1f3bbcc874f0cc160381a611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365899"
---
# <a name="fsrtlexitfilesystem-function"></a>FsRtlExitFileSystem 函数


**FsRtlExitFileSystem**宏将重新启用的普通的内核模式中禁用了前面的调用的 Apc 传递[ **FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FsRtlExitFileSystem(
   VOID 
);
```

<a name="parameters"></a>Parameters
----------

**   
无

<a name="return-value"></a>返回值
------------

此函数不返回值。

<a name="remarks"></a>备注
-------

必须调用每个文件系统驱动程序入口点例程[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)立即才会获取在执行文件 I/O 所需的资源请求并调用**FsRtlExitFileSystem**此后立即。 这可确保不能暂停该例程，但正在运行，因此其他块文件 I/O 请求。

每次成功调用[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)的后续调用必须匹配**FsRtlExitFileSystem**。

请注意，与本地文件系统和网络重定向程序，不同文件系统筛选器驱动程序应永远不会禁用正常内核 Apc 的传递 (通过调用[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)或[**KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)或通过提升到 IRQL APC\_级别) 调用跨[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

文件系统筛选器驱动程序时应禁用正常内核 Apc 的唯一情况是在调用之前立即[ **ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)， [ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)， [ **ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)， [ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)，或[ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)。 在调用[ **ExReleaseResource** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)或[ **ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)，筛选器驱动程序应立即重新启用交付正常内核 Apc。 作为一种替代方法[ **FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)，可以使用微筛选器驱动程序[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)， [ **FltAcquireResourceShared**](fltacquireresourceshared.md)，并[ **FltReleaseResource** ](fltreleaseresource.md)获取时正确处理 Apc 的例程和释放资源。

不需要禁用然后再调用正常内核 Apc [ **ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370)由于此例程调用[ **KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)，它表示禁用这两个正常和特殊内核 Apc。 它不是也这样做之前，先[ **ExAcquireFastMutex** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))或[ **ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)，因为这些例程禁用正常内核 Apc。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))

[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

[**ExReleaseResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)

[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)

 

 






