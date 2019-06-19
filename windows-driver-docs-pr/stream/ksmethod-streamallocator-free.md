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
ms.openlocfilehash: 1ea5f1a2a2581ac5da3f8d0f66eef87aabf53764
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161525"
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
    &Method,
    sizeof(KSMETHOD),
    &Frame,
    sizeof( PVOID ),
    &BytesReturned,
    &Overlapped);
```

 

 





