---
title: EFI_USB_CONFIG_INFO
description: EFI_USB_CONFIG_INFO
ms.assetid: 74d5cb02-2648-4bd1-990e-61156b5dc8cd
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 10ae4734244bc6fa4f5f1ae6d0cdb8511a5788c6
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778329"
---
# <a name="efi_usb_config_info"></a>EFI \_ USB \_ 配置 \_ 信息

**EFI \_ usb \_ 配置 \_ 信息**结构用于定义支持的 usb 端口配置。

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

## <a name="remarks"></a>注解

结构**USB \_ 配置 \_ 描述符**在 UEFI 规范2.3 中定义。 有关详细信息，请访问[UEFI.org](https://uefi.org/specifications)网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
