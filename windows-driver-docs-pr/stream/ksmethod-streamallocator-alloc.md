---
title: KSMETHOD \_ STREAMALLOCATOR \_ 分配
description: KSMETHOD \_ STREAMALLOCATOR \_ 分配方法供客户端用来从给定分配器分配帧。
keywords:
- KSMETHOD_STREAMALLOCATOR_ALLOC 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_STREAMALLOCATOR_ALLOC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86013e04ba1cdd3e4322c6e80fc65ac4dbcbe77c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825341"
---
# <a name="ksmethod_streamallocator_alloc"></a>KSMETHOD \_ STREAMALLOCATOR \_ 分配


**KSMETHOD \_ STREAMALLOCATOR \_ 分配** 方法供客户端用来从给定分配器分配帧。 \_如果当前没有可用的帧，则方法返回状态 "挂起"。 否则，该方法将返回一个指向帧的指针。

例如，内核模式客户端可以使用以下示例代码来分配帧：

<a name="remarks"></a>备注
-------

```cpp
Method.Identifier.Set = KSMETHODSETID_StreamAllocator;
Method.Identifier.Id = KSMETHOD_STREAMALLOCATOR_ALLOC;
Method.Flags = KSMETHOD_TYPE_WRITE;
DeviceIoControl(
    AllocatorHandle,
    IOCTL_KS_METHOD,
    &Method,
    sizeof(KSMETHOD),
    &Frame,
    sizeof(PVOID),
    &BytesReturned,
    &Overlapped);
```

 

 





