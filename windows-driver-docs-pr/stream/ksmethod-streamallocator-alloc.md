---
title: KSMETHOD\_STREAMALLOCATOR\_分配
description: KSMETHOD\_STREAMALLOCATOR\_客户端使用分配方法从给定的分配器分配一个帧。
ms.assetid: 4104d7df-1cc6-4109-9732-220b1065ee01
keywords:
- KSMETHOD_STREAMALLOCATOR_ALLOC 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_STREAMALLOCATOR_ALLOC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af231adc4245019e460aed8f19b0b4234dabce3f
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161530"
---
# <a name="ksmethodstreamallocatoralloc"></a>KSMETHOD\_STREAMALLOCATOR\_分配


**KSMETHOD\_STREAMALLOCATOR\_ALLOC**方法由客户端用来从给定的分配器分配一个帧。 该方法将返回状态\_PENDING 如果目前没有帧。 否则，该方法返回一个指针，到框架。

例如，内核模式下客户端可以使用下面的示例代码来分配一个帧：

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

 

 





