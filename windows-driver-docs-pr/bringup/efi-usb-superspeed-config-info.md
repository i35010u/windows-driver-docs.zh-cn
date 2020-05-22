---
title: EFI_USB_SUPERSPEED_CONFIG_INFO
description: EFI_USB_SUPERSPEED_CONFIG_INFO
ms.assetid: 9827B0A9-AC69-43FA-922F-384E3AE140F7
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 82dd63ae4989f03550f11d4d1a37aff86db994df
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778327"
---
# <a name="efi_usb_superspeed_config_info"></a>EFI \_ USB \_ SUPERSPEED \_ CONFIG \_ 信息

**EFI \_ USB \_ SUPERSPEED \_ 配置 \_ 信息**结构用于定义 USB 功能驱动程序支持的 usb SUPERSPEED 端口配置。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_SUPERSPEED_INTERFACE_INFO   **InterfaceInfoTable;
} EFI_USB_SUPERSPEED_CONFIG_INFO;
```

## <a name="members"></a>成员

### <a name="configdescriptor"></a>ConfigDescriptor

一个 EFI \_ usb \_ 配置 \_ 描述符结构，其中包含 USB 功能设备的配置描述符。

### <a name="interfaceinfotable"></a>InterfaceInfoTable

描述支持的 USB SuperSpeed 接口的[EFI \_ USB \_ SUPERSPEED \_ 接口 \_ 信息](efi-usb-superspeed-interface-info.md)结构。

## <a name="remarks"></a>注解

在 UEFI 规范版本2.3 及更高版本中定义了**EFI \_ USB \_ 配置 \_ 描述符**结构。 有关详细信息，请访问[UEFI.org](https://uefi.org/specifications)网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
