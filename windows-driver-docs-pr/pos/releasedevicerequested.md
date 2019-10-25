---
title: ReleaseDeviceRequested
description: 当另一个客户端尝试声明设备时，将发生 ReleaseDeviceRequested 事件。
ms.assetid: 0fcb8905-1370-4260-9456-6c80e2186dfc
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: c10303ea75da385166f55706dc75a139a18623b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845264"
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
| 0x00000008 | sizeof （**PosEventDataHeader**）                       |

## <a name="remarks"></a>备注

此事件由服务类扩展（PosCx）的点代表设备驱动程序进行处理。 当客户端尝试声明其他客户端正在使用的设备时，PosCx 会在客户端上引发此事件，该事件当前在扫描仪设备上有一个声明，以指示另一个客户端正在尝试声明设备。 当前客户端应保留其声明（[\_服务\_保留\_设备的 ioctl\_点\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_retain_device)）或释放其声明（[\_服务\_版本\_的 ioctl\_点\_设备](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ni-pointofservicedriverinterface-ioctl_point_of_service_release_device)）来响应此事件。 如果当前客户端未在设备上保留其声明，则其**ClaimedBarcodeScanner**对象将不再有效。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
