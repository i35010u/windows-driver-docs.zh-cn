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
ms.openlocfilehash: fc978daf2a07eea91ea8eb5aff16f1b5a810a2eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543313"
---
# <a name="registering-fsfilter-callback-routines"></a>注册 FsFilter 回调例程


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


之前和之后基础文件系统将执行某些操作称为 FsFilter 通知回调例程。 有关 FsFilter 回调例程的详细信息，请参阅[ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)。

若要注册 FsFilter 通知回调例程，必须分配并初始化与 FS\_筛选器\_回调结构、 在结构中，存储 FsFilter 回调例程的入口点，将传递的地址结构中*回叫*参数**FsRtlRegisterFileSystemFilterCallbacks**。

例如，假设"MyLegacyFilter"驱动程序可以按如下所示注册其 FsFilter 回调例程：

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

 

 




