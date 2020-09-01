---
title: ReleaseDeviceRequested
description: 当另一个客户端尝试声明设备时，将发生 ReleaseDeviceRequested 事件。
ms.assetid: 0fcb8905-1370-4260-9456-6c80e2186dfc
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4d238c90979e7abe2449f610190e6bb59e52a07b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192903"
---
# <a name="releasedevicerequested"></a>ReleaseDeviceRequested

当另一个客户端尝试声明设备时发生此事件。 此事件的数据缓冲区如下所示。

## <a name="syntax"></a>语法

```cpp
typedef struct _PosEventDataHeader
{
    // Event enumeration value
    PosEventType EventType;

    // Size of buffer required to read entire event (including header)
    UINT32 DataLength;
} PosEventDataHeader;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值          | 描述                               |
|-----------------------|-------------------------------------------|
| 0x00000001 | **事件 = PosEventType：： ReleaseDeviceRequested** |
| 0x00000008 | sizeof (**PosEventDataHeader**)                        |

## <a name="remarks"></a>备注

此事件由服务类扩展 (PosCx) 的点，代表设备驱动程序进行处理。 当客户端尝试声明其他客户端正在使用的设备时，PosCx 会在客户端上引发此事件，该事件当前在扫描仪设备上有一个声明，以指示另一个客户端正在尝试声明设备。 当前客户端应将其声明保留 (" [ \_ \_ \_ 服务 \_ 保留 \_ 设备的 ioctl 点](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_retain_device) ") 或释放其声明 (的 [ioctl) \_ 点 \_ \_ \_ \_ ](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_release_device) ，以响应此事件。 如果当前客户端未在设备上保留其声明，则其 **ClaimedBarcodeScanner** 对象将不再有效。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface