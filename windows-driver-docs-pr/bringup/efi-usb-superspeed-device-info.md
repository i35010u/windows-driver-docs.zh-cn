---
title: EFI_USB_SUPERSPEED_DEVICE_INFO
description: EFI_USB_SUPERSPEED_DEVICE_INFO
ms.assetid: 7861BA16-7499-48A1-9D6A-9BB8F5AA36CE
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: a059ff06fc2359c2a9ae62a0e3d25fae6476039f
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778330"
---
# <a name="efi_usb_superspeed_device_info"></a>EFI \_ USB \_ SUPERSPEED \_ 设备 \_ 信息

**EFI \_ usb \_ SUPERSPEED \_ 设备 \_ 信息**结构用于定义 USB SUPERSPEED 函数设备。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_SUPERSPEED_CONFIG_INFO      **ConfigInfoTable;
    EFI_USB_BOS_DESCRIPTOR              *BosDescriptor
} EFI_USB_SUPERSPEED_DEVICE_INFO;
```

## <a name="members"></a>成员

### <a name="devicedescriptor"></a>DeviceDescriptor

EFI \_ usb \_ 设备 \_ 描述符结构，其中包含 USB 设备的配置信息。

### <a name="configinfotable"></a>ConfigInfoTable

[EFI \_ usb \_ SUPERSPEED \_ 配置 \_ 信息](efi-usb-superspeed-config-info.md)结构，其中包含有关受支持的 USB SUPERSPEED 配置的信息。

### <a name="bosdescriptor"></a>BosDescriptor

[EFI \_ usb \_ BOS \_ 描述符](efi-usb-bos-descriptor.md)结构，其中包含有关二进制对象存储到 USB 函数驱动程序的信息。

## <a name="remarks"></a>注解

在 UEFI 规范版本2.3 及更高版本中定义了**EFI \_ USB \_ 配置 \_ 描述符**结构。 有关详细信息，请访问[UEFI.org](https://uefi.org/specifications)网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
