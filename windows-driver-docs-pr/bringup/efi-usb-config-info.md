---
title: EFI_USB_CONFIG_INFO
description: EFI_USB_CONFIG_INFO
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6eda4d0158ee6440491494ca9058ab0c3100fc2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789075"
---
# <a name="efi_usb_config_info"></a>EFI \_ USB \_ 配置 \_ 信息

**EFI \_ usb \_ 配置 \_ 信息** 结构用于定义支持的 usb 端口配置。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_INTERFACE_INFO              **InterfaceInfoTable;
} EFI_USB_CONFIG_INFO;
```

## <a name="members"></a>成员

### <a name="configdescriptor"></a>ConfigDescriptor

EFI \_ usb \_ 配置 \_ 描述符结构，其中包含 USB 功能设备的配置信息。

### <a name="interfaceinfotable"></a>InterfaceInfoTable

[EFI \_ USB \_ 接口 \_ 信息](efi-usb-interface-info.md)结构，其中包含有关支持的接口的信息。

## <a name="remarks"></a>备注

结构 **USB \_ 配置 \_ 描述符** 在 UEFI 规范2.3 中定义。 有关详细信息，请访问 [UEFI.org](https://uefi.org/specifications) 网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
