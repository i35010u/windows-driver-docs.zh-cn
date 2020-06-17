---
title: POOL_FLAGS
description: 标志，用于指示池内存的类型、需要内存的属性，以及可以选择的内存属性。
ms.assetid: 1eaee689-69fb-4720-adbc-b9db5fdc113a
keywords:
- 内存管理 WDK 内核，系统分配的空间
- 系统分配的空间 WDK 内核
- 分配系统空间内存
- 分配 i/o 缓冲区内存
- I/o 缓冲内存分配 WDK 内核
- 缓冲区内存分配 WDK 内核
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e8c4c6a8d5f305af00d5e649de9e14e282c47a2
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882324"
---
# <a name="pool_flags"></a>POOL_FLAGS

ULONG64 类型的值，指定池内存的类型以及必需和可选属性。 可以使用按位 "或" 组合多个标志值。

```cpp
//
// POOL_FLAG values
//
// Low 32-bits of ULONG64 are for required parameters (allocation fails if they
// cannot be satisfied).
// High 32-bits of ULONG64 is for optional parameters (allocation succeeds if
// they cannot be satisfied or are unrecognized).
//

#define POOL_FLAG_REQUIRED_START          0x0000000000000001UI64
#define POOL_FLAG_USE_QUOTA               0x0000000000000001UI64     // Charge quota
#define POOL_FLAG_UNINITIALIZED           0x0000000000000002UI64     // Don't zero-initialize allocation
#define POOL_FLAG_SESSION                 0x0000000000000004UI64     // Use session specific pool
#define POOL_FLAG_CACHE_ALIGNED           0x0000000000000008UI64     // Cache aligned allocation
#define POOL_FLAG_RESERVED1               0x0000000000000010UI64     // Reserved for system use
#define POOL_FLAG_RAISE_ON_FAILURE        0x0000000000000020UI64     // Raise exception on failure
#define POOL_FLAG_NON_PAGED               0x0000000000000040UI64     // Non paged pool NX
#define POOL_FLAG_NON_PAGED_EXECUTE       0x0000000000000080UI64     // Non paged pool executable
#define POOL_FLAG_PAGED                   0x0000000000000100UI64     // Paged pool
#define POOL_FLAG_RESERVED2               0x0000000000000200UI64     // Reserved for system use
#define POOL_FLAG_RESERVED3               0x0000000000000400UI64     // Reserved for system use
#define POOL_FLAG_REQUIRED_END            0x0000000080000000UI64
#define POOL_FLAG_OPTIONAL_START          0x0000000100000000UI64
#define POOL_FLAG_SPECIAL_POOL            0x0000000100000000UI64     // Make special pool allocation
#define POOL_FLAG_OPTIONAL_END            0x8000000000000000UI64
```

## <a name="required-flags"></a>必需标志

池分配器必须识别和满足必需的标志。 如果分配器不能识别该标志或无法进行分配，则分配将失败。

|名称|说明|
|-|-|
|POOL_FLAG_USE_QUOTA|此标志由最高层驱动程序传递，该驱动程序分配内存以满足最初发出 i/o 请求的进程上下文中的请求。 较低级别的驱动程序无需指定此标志。|
|POOL_FLAG_UNINITIALIZED|使分配保持未初始化状态。 分配的内容为 indeterminant。 驱动程序必须非常小心，切勿将未初始化的内存复制到不受信任的目标（用户模式，通过网络等）。|
|POOL_FLAG_SESSION|为操作系统保留。|
|POOL_FLAG_CACHE_ALIGNED|缓存对齐池分配。 警告：此标志被视为最佳工作，如果程序的正确性需要缓存对齐分配，则不应使用此标志。|
|POOL_FLAG_RESERVED1|保留以供内部使用。|
|POOL_FLAG_RAISE_ON_FAILURE|如果无法满足分配，则引发异常。|
|POOL_FLAG_NON_PAGED|在非分页池中进行分配。|
|POOL_FLAG_NON_PAGED_EXECUTE|在未分页的可执行文件池中进行分配。|
|POOL_FLAG_PAGED|在分页池中进行分配。 这是对所有其他平台上的 x86、不可执行的可执行文件。|
|POOL_FLAG_RESERVED2|保留以供内部使用。|
|POOL_FLAG_RESERVED3|保留以供内部使用。|

## <a name="optional-flags"></a>可选标志

池分配器找机会满足了可选标志。 如果分配器不识别可选标志，则将其忽略。 如果分配器无法满足可选标志，则它可能会也可能不会成功，具体取决于特定标志的语义。

|名称|说明|
|-|-|
|POOL_FLAG_SPECIAL_POOL|在特殊池中进行分配（用于调试）。 如果无法使用特殊池，则分配器将尝试使用常规池。|

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| ---- |:---- |
|标题|wdm .h （包括 Wdm、Ntddk、Ntifs、Wudfwdm）。|

## <a name="see-also"></a>另请参阅

[**ExAllocatePool2**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2)
