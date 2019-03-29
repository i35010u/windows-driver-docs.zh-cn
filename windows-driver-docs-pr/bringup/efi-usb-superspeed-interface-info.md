---
title: EFI_USB_SUPERSPEED_INTERFACE_INFO
description: EFI_USB_SUPERSPEED_INTERFACE_INFO
ms.assetid: 1B0C04D0-5254-4B9A-A94D-4FF1CEAD4627
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e4b98501f0e99df7bec364d6ff1a91ff2d47d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564826"
---
# <a name="efiusbsuperspeedinterfaceinfo"></a>EFI\_USB\_SUPERSPEED\_INTERFACE\_INFO


**EFI\_USB\_SUPERSPEED\_接口\_信息**结构用于定义 USB 功能驱动程序支持的 USB SuperSpeed 接口。

## <a name="syntax"></a>语法


```cpp
typedef struct
{
    EFI_USB_INTERFACE_DESCRIPTOR            *InterfaceDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR  **EndpointDescriptorTable; 
} EFI_USB_SUPERSPEED_INTERFACE_INFO;
```

## <a name="members"></a>成员


<a href="" id="interfacedescriptor"></a>**InterfaceDescriptor**  
EFI\_USB\_接口\_描述符结构描述 USB 函数接口。

<a href="" id="endpointdescriptortable"></a>**EndpointDescriptorTable**  
[EFI\_USB\_SUPERSPEED\_终结点\_描述符](efi-usb-superspeed-endpoint-descriptor.md)介绍 USB SuperSpeed 终结点的结构。

## <a name="remarks"></a>备注


**EFI\_USB\_界面\_描述符**结构是定义中的 UEFI 规范版本 2.3 及更高版本。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




