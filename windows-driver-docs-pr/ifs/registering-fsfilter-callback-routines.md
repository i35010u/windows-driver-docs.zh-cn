---
title: 注册 FsFilter 回调例程
description: 注册 FsFilter 回调例程
ms.assetid: d040e61c-514e-446b-9e72-934fd4322d3b
keywords:
- 注册回调例程
- 回调例程 WDK 文件系统
- FsFilter 通知回调例程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d2bb0491d0762e5e10983aea14e155d8d0fdc83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841006"
---
# <a name="registering-fsfilter-callback-routines"></a>注册 FsFilter 回调例程


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


在基础文件系统执行特定操作之前和之后，将调用 FsFilter 通知回调例程。 有关 FsFilter 回调例程的详细信息，请参阅[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)。

若要注册 FsFilter 通知回调例程，必须分配和初始化 FS\_筛选器\_回调结构，将 FsFilter 回调例程的入口点存储到结构中，并在**FsRtlRegisterFileSystemFilterCallbacks**的*回调*参数。

例如，假设 "MyLegacyFilter" 驱动程序可以注册其 FsFilter 回调例程，如下所示：

```cpp
fsFilterCallbacks.SizeOfFsFilterCallbacks = sizeof(FS_FILTER_CALLBACKS);
fsFilterCallbacks.PreAcquireForSectionSynchronization = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostAcquireForSectionSynchronization = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreReleaseForSectionSynchronization = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostReleaseForSectionSynchronization = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreAcquireForCcFlush = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostAcquireForCcFlush = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreReleaseForCcFlush = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostReleaseForCcFlush = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreAcquireForModifiedPageWriter = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostAcquireForModifiedPageWriter = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreReleaseForModifiedPageWriter = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostReleaseForModifiedPageWriter = MyLegacyFilterPostFsFilterOperation;

status = FsRtlRegisterFileSystemFilterCallbacks(DriverObject, &fsFilterCallbacks);
```

 

 




