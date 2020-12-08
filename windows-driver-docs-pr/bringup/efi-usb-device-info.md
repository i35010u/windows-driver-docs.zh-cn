---
title: EFI_USB_DEVICE_INFO
description: EFI_USB_DEVICE_INFO
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: ffbf85e39b2b9c7b752c40d01cc3bb5d42f30be4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803391"
---
# <a name="efi_usb_device_info"></a>EFI \_ USB \_ 设备 \_ 信息

**EFI \_ usb \_ 设备 \_ 信息** 结构用于定义 USB 函数设备。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_CONFIG_INFO                 **ConfigInfoTable;
} EFI_USB_DEVICE_INFO;
```

## <a name="members"></a>成员

### <a name="devicedescriptor"></a>DeviceDescriptor

EFI \_ usb \_ 设备 \_ 描述符结构，其中包含 USB 设备的配置信息。

### <a name="configinfotable"></a>ConfigInfoTable

EFI \_ USB \_ 配置 \_ 信息结构，其中包含有关支持的配置的信息。

## <a name="remarks"></a>备注

在 UEFI 规范2.3 中定义了 **efi \_ usb \_ 配置 \_ 描述符** 和 **efi \_ usb \_ 设备 \_ 描述符** 结构。 有关详细信息，请访问 [UEFI.org](https://uefi.org/specifications) 网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
