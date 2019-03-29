---
title: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
ms.assetid: 3254C0F1-85C2-472B-938A-F71645703540
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707369e918301a1b1f3387e6253a8235b078a119
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575470"
---
# <a name="efiusbsuperspeedendpointdescriptor"></a>EFI\_USB\_SUPERSPEED\_终结点\_描述符


**EFI\_USB\_SUPERSPEED\_终结点\_描述符**结构用于描述对 USB 函数驱动程序支持的 USB SuperSpeed 终结点。

## <a name="syntax"></a>语法


```cpp
typedef struct
{
    EFI_USB_ENDPOINT_DESCRIPTOR                         *EndpointDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR    *EndpointCompanionDescriptor;
} EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR;
```

## <a name="members"></a>成员


<a href="" id="endpointdescriptor"></a>**EndpointDescriptor**  
EFI\_USB\_终结点\_描述符结构，它介绍 USB 终结点。

<a href="" id="endpointcompaniondescriptor"></a>**EndpointCompanionDescriptor**  
[EFI\_USB\_SUPERSPEED\_终结点\_配套\_描述符](efi-usb-superspeed-endpoint-companion-descriptor.md)结构，它是 USB SuperSpeed 终结点的配套描述符。

## <a name="remarks"></a>备注


**EFI\_USB\_终结点\_描述符**结构是定义中的 UEFI 规范版本 2.3 及更高版本。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




