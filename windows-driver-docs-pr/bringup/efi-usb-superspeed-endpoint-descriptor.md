---
title: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
ms.assetid: 3254C0F1-85C2-472B-938A-F71645703540
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb9670a81c73ab3f33b0308a1a54a95daf495d94
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778337"
---
# <a name="efi_usb_superspeed_endpoint_descriptor"></a>EFI \_ USB \_ SUPERSPEED \_ 终结点 \_ 描述符

**EFI \_ USB \_ SUPERSPEED \_ 终结点 \_ 描述符**结构用于介绍 USB 函数驱动程序支持的 usb SUPERSPEED 终结点。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
    EFI_USB_ENDPOINT_DESCRIPTOR                         *EndpointDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR    *EndpointCompanionDescriptor;
} EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR;
```

## <a name="members"></a>成员

### <a name="endpointdescriptor"></a>EndpointDescriptor

\_ \_ 描述 USB 端点的 EFI USB 终结点 \_ 描述符结构。

### <a name="endpointcompaniondescriptor"></a>EndpointCompanionDescriptor

[EFI \_ usb \_ SUPERSPEED \_ 终结点 \_ 伴随 \_ 描述符](efi-usb-superspeed-endpoint-companion-descriptor.md)结构，是 USB SUPERSPEED 终结点的伴随描述符。

## <a name="remarks"></a>注解

在 UEFI 规范版本2.3 及更高版本中定义了**EFI \_ USB \_ 终结点 \_ 描述符**结构。 有关详细信息，请访问[UEFI.org](https://uefi.org/specifications)网站。

## <a name="requirements"></a>要求

**标头：** 用户生成
