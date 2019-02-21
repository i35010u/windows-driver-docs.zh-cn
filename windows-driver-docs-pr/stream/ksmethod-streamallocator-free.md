---
title: KSMETHOD\_STREAMALLOCATOR\_免费
description: KSMETHOD\_STREAMALLOCATOR\_客户端使用免费的方法来释放回发到给定的分配器的帧。
ms.assetid: 90d42ae6-4aa2-46fd-b10c-7f07b77c86f1
keywords:
- KSMETHOD_STREAMALLOCATOR_FREE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_STREAMALLOCATOR_FREE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5026b0a0193e7ed1918e7837083a562d5d567d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519556"
---
# <a name="ksmethodstreamallocatorfree"></a>KSMETHOD\_STREAMALLOCATOR\_免费


**KSMETHOD\_STREAMALLOCATOR\_免费**客户端使用方法来释放回发到给定的分配器的帧。 挂起[ **KSMETHOD\_STREAMALLOCATOR\_分配**](ksmethod-streamallocator-alloc.md)，如果任何，可以使用此方法已完成。

例如，内核模式下客户端可以使用下面的示例代码来释放帧：

<a name="remarks"></a>备注
-------

```cpp
Method.Identifier.Set = KSMETHODSETID_StreamAllocator;
Method.Identifier.Id = KSMETHOD_STREAMALLOCATOR_FREE;
Method.Flags = KSMETHOD_TYPE_READ;
DeviceIoControl(
    AllocatorHandle,
    IOCTL_KS_METHOD,
    &amp;Method,
    sizeof(KSMETHOD),
    &amp;Frame,
    sizeof( PVOID ),
    &amp;BytesReturned,
    &amp;Overlapped);
```

 

 





