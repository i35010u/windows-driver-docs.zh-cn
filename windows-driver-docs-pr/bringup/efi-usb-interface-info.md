---
title: EFI_USB_INTERFACE_INFO
description: EFI_USB_INTERFACE_INFO
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 020d735dd717810e68120744be39ca240b9cf372
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803389"
---
# <a name="efi_usb_interface_info"></a>EFI \_ USB \_ 接口 \_ 信息

**EFI \_ usb \_ 接口 \_ 信息** 结构，用于定义支持的 USB 接口。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_INTERFACE_DESCRIPTOR        *InterfaceDescriptor;
    EFI_USB_ENDPOINT_DESCRIPTOR         **EndpointDescriptorTable;
} EFI_USB_INTERFACE_INFO;
```

## <a name="members"></a>成员

### <a name="interfacedescriptor"></a>InterfaceDescriptor

EFI \_ usb \_ 接口 \_ 描述符结构，其中包含有关 USB 函数接口的信息。

### <a name="endpointdescriptortable"></a>EndpointDescriptorTable

EFI \_ USB \_ 终结点 \_ 描述符结构，其中包含有关支持的终结点的信息。

## <a name="remarks"></a>备注

在 UEFI 规范2.3 中定义 **usb \_ 接口 \_ 描述符** 和 **usb \_ 终结点 \_ 描述符** 结构。 有关详细信息，请访问 [UEFI.org](https://uefi.org/specifications) 网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
