---
title: FsRtlEnterFileSystem 函数
description: FsRtlEnterFileSystem 宏暂时禁用普通的内核模式下异步过程调用 (APC) 的传递。 仍提供特殊的内核模式 Apc。
ms.assetid: 6aa6315d-e430-4189-8eb5-9427a2e5ba46
keywords:
- FsRtlEnterFileSystem 函数可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FsRtlEnterFileSystem
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68f2d21a9d6f91e869851da710940d0095bb0460
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565327"
---
# <a name="fsrtlenterfilesystem-function"></a>FsRtlEnterFileSystem 函数


**FsRtlEnterFileSystem**宏暂时禁用的普通的内核模式下异步过程调用 (APC) 传递。 仍提供特殊的内核模式 Apc。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FsRtlEnterFileSystem(
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

必须调用每个文件系统驱动程序入口点例程**FsRtlEnterFileSystem**立即才会获取在执行文件 I/O 所需的资源请求并调用[ **FsRtlExitFileSystem**](fsrtlexitfilesystem.md)此后立即。 这可确保不能暂停该例程，但正在运行，因此其他块文件 I/O 请求。

每次成功调用**FsRtlEnterFileSystem**的后续调用必须匹配[ **FsRtlExitFileSystem**](fsrtlexitfilesystem.md)。

请注意，与本地文件系统和网络重定向程序，不同文件系统筛选器驱动程序应永远不会禁用正常内核 Apc 的传递 (通过调用**FsRtlEnterFileSystem**或[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)或通过提升到 IRQL APC\_级别) 调用跨[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。

文件系统筛选器驱动程序应获取任何资源之前禁用正常内核 Apc。 文件系统筛选器驱动程序中获取以下例程使用的资源：

-   [**ExAcquireResourceExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544345)

-   [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

-   [**ExAcquireResourceShared**](https://msdn.microsoft.com/library/windows/hardware/ff544359)

-   [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

-   [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

-   [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

作为一种替代方法**FsRtlEnterFileSystem**，可以使用微筛选器驱动程序[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)， [ **FltAcquireResourceShared**](fltacquireresourceshared.md)，并[ **FltReleaseResource** ](fltreleaseresource.md)例程可正确处理 Apc 时获得和释放资源。

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


[**ExAcquireResourceExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544345)

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExAcquireResourceShared**](https://msdn.microsoft.com/library/windows/hardware/ff544359)

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

[**ExReleaseResource**](https://msdn.microsoft.com/library/windows/hardware/ff545571)

[**ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)

[**ExTryToAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545647)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)

[**KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084)

 

 






