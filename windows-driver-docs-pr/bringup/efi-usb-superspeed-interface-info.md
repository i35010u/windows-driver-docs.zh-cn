---
title: EFI_USB_SUPERSPEED_INTERFACE_INFO
description: EFI_USB_SUPERSPEED_INTERFACE_INFO
ms.assetid: 1B0C04D0-5254-4B9A-A94D-4FF1CEAD4627
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5b25187ba0193cd30e58316f6caa7780faa6f83e
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778325"
---
# <a name="efi_usb_superspeed_interface_info"></a>EFI \_ USB \_ SUPERSPEED \_ 接口 \_ 信息

**EFI \_ USB \_ SUPERSPEED \_ 接口 \_ 信息**结构用于定义 usb 函数驱动程序所支持的 usb SUPERSPEED 接口。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_INTERFACE_DESCRIPTOR            *InterfaceDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR  **EndpointDescriptorTable;
} EFI_USB_SUPERSPEED_INTERFACE_INFO;
```

## <a name="members"></a>成员

### <a name="interfacedescriptor"></a>InterfaceDescriptor

\_ \_ \_ 描述 usb 函数接口的 EFI USB 接口描述符结构。

### <a name="endpointdescriptortable"></a>EndpointDescriptorTable

描述 USB SuperSpeed 终结点的[EFI \_ USB \_ SUPERSPEED \_ 终结点 \_ 描述符](efi-usb-superspeed-endpoint-descriptor.md)结构。

## <a name="remarks"></a>注解

**EFI \_ USB \_ 接口 \_ 描述符**结构在 UEFI 规范版本2.3 及更高版本中定义。 有关详细信息，请访问[UEFI.org](https://uefi.org/specifications)网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
