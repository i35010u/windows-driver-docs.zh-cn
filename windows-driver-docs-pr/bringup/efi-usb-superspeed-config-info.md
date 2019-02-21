---
title: EFI_USB_SUPERSPEED_CONFIG_INFO
description: EFI_USB_SUPERSPEED_CONFIG_INFO
ms.assetid: 9827B0A9-AC69-43FA-922F-384E3AE140F7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f336370023fff9ddd185c6c4f2b56140499240a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523724"
---
# <a name="efiusbsuperspeedconfiginfo"></a>EFI\_USB\_SUPERSPEED\_CONFIG\_信息


**EFI\_USB\_SUPERSPEED\_CONFIG\_信息**结构用于对 USB 函数驱动程序定义的受支持的 USB SuperSpeed 端口配置。

## <a name="syntax"></a>语法


```cpp
typedef struct
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_SUPERSPEED_INTERFACE_INFO   **InterfaceInfoTable;
} EFI_USB_SUPERSPEED_CONFIG_INFO;
```

## <a name="members"></a>成员


<a href="" id="configdescriptor"></a>**ConfigDescriptor**  
EFI\_USB\_CONFIG\_描述符结构，其中包含 USB 函数设备的配置描述符。

<a href="" id="interfaceinfotable"></a>**InterfaceInfoTable**  
[EFI\_USB\_SUPERSPEED\_接口\_信息](efi-usb-superspeed-interface-info.md)介绍受支持的 USB SuperSpeed 接口的结构。

## <a name="remarks"></a>备注


**EFI\_USB\_CONFIG\_描述符**结构是定义中的 UEFI 规范版本 2.3 及更高版本。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




