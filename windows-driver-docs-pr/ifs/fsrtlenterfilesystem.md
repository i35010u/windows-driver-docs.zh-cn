---
title: FsRtlEnterFileSystem 函数
description: FsRtlEnterFileSystem 宏暂时禁用 (APC) 的正常内核模式异步过程调用。 还提供了特殊的内核模式 Apc。
date: 06/25/2019
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
ms.openlocfilehash: b7671baf3bc7ebe848f7b4937b3ed8b5fa937cbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821481"
---
# <a name="fsrtlenterfilesystem-function"></a>FsRtlEnterFileSystem 函数

**FsRtlEnterFileSystem** 宏暂时禁用 (APC) 的正常内核模式异步过程调用。 还提供了特殊的内核模式 Apc。

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

每个文件系统驱动程序入口点例程在获取执行文件 i/o 请求所需的资源之前，必须立即调用 **FsRtlEnterFileSystem** ，并立即调用 [**FsRtlExitFileSystem**](fsrtlexitfilesystem.md) 。 这可确保在运行时无法挂起例程，从而阻止其他文件 i/o 请求。

必须通过对 [**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)的后续调用来匹配每个对 **FsRtlEnterFileSystem** 的成功调用。

文件系统筛选器驱动程序可以通过在 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之前调用 **FsRtlEnterFileSystem** 或 [**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)来禁止交付普通内核 apc [**FsRtlExitFileSystem**](./fsrtlexitfilesystem.md) [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 它们不应在 **IoCallDriver** 之前调用 **FsRtlEnterFileSystem** 或 **KeEnterCriticalRegion** ，然后在 IRP 的 *完成例程* 中调用 **FsRtlExitFileSystem** 或 **KeLeaveCriticalRegion** 。 驱动程序验证程序提供了一个有助于捕获此情况的规则。

文件系统筛选器驱动程序应在获取任何资源之前禁用正常内核 Apc。 文件系统筛选器驱动程序通过以下例程获取资源：

* [**ExAcquireResourceExclusive**](../kernel/mmcreatemdl.md)
* [**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))
* [**ExAcquireResourceShared**](../kernel/mmcreatemdl.md)
* [**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))
* [**ExAcquireSharedStarveExclusive**](/previous-versions/ff544367(v=vs.85))
* [**ExAcquireSharedWaitForExclusive**](/previous-versions/ff544370(v=vs.85))

作为 **FsRtlEnterFileSystem** 的一种替代方法，微筛选器驱动程序可以使用 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [**FltAcquireResourceShared**](fltacquireresourceshared.md)和 [**FltReleaseResource**](fltreleaseresource.md) 例程，在获取和释放资源时正确处理 apc。

## <a name="requirements"></a>要求

**目标平台**：桌面

**标头**： Ntifs (包含 Ntifs) 

**IRQL**： <= APC_LEVEL


## <a name="see-also"></a>请参阅

[**ExAcquireResourceExclusive**](../kernel/mmcreatemdl.md)

[**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))

[**ExAcquireResourceShared**](../kernel/mmcreatemdl.md)

[**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))

[**ExAcquireSharedWaitForExclusive**](/previous-versions/ff544370(v=vs.85))

[**ExAcquireSharedStarveExclusive**](/previous-versions/ff544367(v=vs.85))

[**ExReleaseResource**](../kernel/mmcreatemdl.md)

[**ExReleaseResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)

[**ExTryToAcquireFastMutex**](/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

[**KeRaiseIrqlToDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)
