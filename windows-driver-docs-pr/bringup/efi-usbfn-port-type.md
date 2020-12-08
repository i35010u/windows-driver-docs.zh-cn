---
title: EFI_USBFN_PORT_TYPE
description: EFI_USBFN_PORT_TYPE
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 25053c8bb98eb06c55e4e1bf8ba3ce1f0d1982df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789007"
---
# <a name="efi_usbfn_port_type"></a>EFI \_ USBFN \_ 端口 \_ 类型

此枚举指定 USB 端口类型。

## <a name="syntax"></a>语法

```cpp
typedef enum _EFI_USBFN_PORT_TYPE
{
    EfiUsbUnknownPort = 0,
    EfiUsbStandardDownstreamPort,
    EfiUsbChargingDownstreamPort,
    EfiUsbDedicatedChargingPort,
    EfiUsbInvalidDedicatedChargingPort
} EFI_USBFN_PORT_TYPE;
```

## <a name="constants"></a>常量

| “值” | 描述 |
| --- | --- |
| EfiUsbUnknownPort | 未知端口-驱动程序内部默认端口类型;该驱动程序不会使用成功状态代码返回此消息。 |
| EfiUsbStandardDownstreamPort | 标准下游端口-标准 USB 主机。 |
| EfiUsbChargingDownstreamPort | 向下游端口收费-标准 USB 主机。 |
| EfiUsbDedicatedChargingPort | 专用收费端口–一种墙充电器，而不是 USB 主机。 |
| EfiUsbInvalidDedicatedChargingPort | 无效的专用收费端口–非 USB 主机或专用收费端口。 |

## <a name="remarks"></a>备注

有关详细信息，请参阅 [USB.org](https://www.usb.org/documents) 网站上的 "电池充电规范，修订版本 1.1"。

## <a name="requirements"></a>要求

**标头：** 用户生成
