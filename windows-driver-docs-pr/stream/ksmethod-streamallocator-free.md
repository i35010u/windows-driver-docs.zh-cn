---
title: KSMETHOD \_ STREAMALLOCATOR \_ 免费
description: '\_ \_ 客户端使用 KSMETHOD STREAMALLOCATOR free 方法将帧释放回给定分配器。'
keywords:
- KSMETHOD_STREAMALLOCATOR_FREE 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_STREAMALLOCATOR_FREE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bc4a0068ce9b179c669638d5d8f2df769bd14ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825343"
---
# <a name="ksmethod_streamallocator_free"></a>KSMETHOD \_ STREAMALLOCATOR \_ 免费


客户端使用 **KSMETHOD \_ STREAMALLOCATOR \_ free** 方法将帧释放回给定分配器。 挂起的 [**KSMETHOD \_ STREAMALLOCATOR \_ 分配**](ksmethod-streamallocator-alloc.md)（如果有）可以通过使用此方法来完成。

例如，内核模式客户端可以使用以下示例代码来释放帧：

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

 

 





