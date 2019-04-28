---
title: ReleaseDeviceRequested
description: 另一个客户端尝试声明设备时发生 ReleaseDeviceRequested 事件。
ms.assetid: 0fcb8905-1370-4260-9456-6c80e2186dfc
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc0d485ed5e1946954b309cb62941a7dc7984b2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349303"
---
# <a name="releasedevicerequested"></a>ReleaseDeviceRequested

当另一个客户端尝试声明设备时，将发生此事件。 此事件的数据缓冲区是按如下所示。

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

下表显示了此事件的数据缓冲区的内存布局。

| 内存值          | 描述                               |
|-----------------------|-------------------------------------------|
| 0x00000001 | **事件类型 = PosEventType::ReleaseDeviceRequested** |
| 0x00000008 | sizeof(**PosEventDataHeader**)                       |

## <a name="remarks"></a>备注

此事件的代表的设备驱动程序处理的点的服务类扩展 (PosCx)。 当客户端尝试声明另一个客户端使用的设备时，PosCx 引发此事件在当前拥有扫描程序设备上的声明，以指示另一个客户端正在尝试声明该设备的客户端。 当前客户端应可以保留其声明 ([IOCTL\_点\_OF\_服务\_保留\_设备](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_retain_device)) 或释放其声明 ([IOCTL\_点\_OF\_服务\_发行\_设备](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_release_device)) 以响应此事件的设备。 如果当前的客户端不会保留在设备上，其声明其**ClaimedBarcodeScanner**对象将不再有效。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
