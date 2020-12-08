---
title: 注册 FsFilter 回调例程
description: 注册 FsFilter 回调例程
keywords:
- 注册回调例程
- 回调例程 WDK 文件系统
- FsFilter 通知回调例程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d71dcb67a2aca1cae11b973e13965a96bc15474f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840727"
---
# <a name="registering-fsfilter-callback-routines"></a>注册 FsFilter 回调例程


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


在基础文件系统执行特定操作之前和之后，将调用 FsFilter 通知回调例程。 有关 FsFilter 回调例程的详细信息，请参阅 [**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)。

若要注册 FsFilter 通知回调例程，必须分配和初始化 FS \_ 筛选器 \_ 回调结构，将 FsFilter 回调例程的入口点存储到结构中，并将 *回调* 参数中结构的地址传递给 **FsRtlRegisterFileSystemFilterCallbacks**。

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

 

