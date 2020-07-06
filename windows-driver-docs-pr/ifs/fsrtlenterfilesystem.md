---
title: FsRtlEnterFileSystem 函数
description: FsRtlEnterFileSystem 宏暂时禁用正常内核模式异步过程调用（APC）的传送。 还提供了特殊的内核模式 Apc。
date: 06/25/2019
ms.assetid: 6aa6315d-e430-4189-8eb5-9427a2e5ba46
keywords:
- FsRtlEnterFileSystem 函数可安装的文件系统驱动程序
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
ms.openlocfilehash: 01e104146823bafaaa695cbf333dfdae4cb36a0b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968208"
---
# <a name="fsrtlenterfilesystem-function"></a>FsRtlEnterFileSystem 函数

**FsRtlEnterFileSystem**宏暂时禁用正常内核模式异步过程调用（APC）的传送。 还提供了特殊的内核模式 Apc。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
VOID FsRtlEnterFileSystem(
   VOID
);
```

## <a name="parameters"></a>参数

None

## <a name="return-value"></a>返回值

此函数不返回值。

## <a name="remarks"></a>备注

每个文件系统驱动程序入口点例程在获取执行文件 i/o 请求所需的资源之前，必须立即调用**FsRtlEnterFileSystem** ，并立即调用[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md) 。 这可确保在运行时无法挂起例程，从而阻止其他文件 i/o 请求。

必须通过对[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)的后续调用来匹配每个对**FsRtlEnterFileSystem**的成功调用。

文件系统筛选器驱动程序可以通过在[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之前调用**FsRtlEnterFileSystem**或[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)来禁止交付普通内核 apc [**FsRtlExitFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem) [**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 它们不应在**IoCallDriver**之前调用**FsRtlEnterFileSystem**或**KeEnterCriticalRegion** ，然后在 IRP 的*完成例程*中调用**FsRtlExitFileSystem**或**KeLeaveCriticalRegion** 。 驱动程序验证程序提供了一个有助于捕获此情况的规则。

文件系统筛选器驱动程序应在获取任何资源之前禁用正常内核 Apc。 文件系统筛选器驱动程序通过以下例程获取资源：

* [**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
* [**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)
* [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
* [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

作为**FsRtlEnterFileSystem**的一种替代方法，微筛选器驱动程序可以使用[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [**FltAcquireResourceShared**](fltacquireresourceshared.md)和[**FltReleaseResource**](fltreleaseresource.md)例程，在获取和释放资源时正确处理 apc。

## <a name="requirements"></a>要求

**目标平台**：桌面

**标头**： Ntifs （包括 Ntifs）

**IRQL**： <= APC_LEVEL


## <a name="see-also"></a>另请参阅

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

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)
