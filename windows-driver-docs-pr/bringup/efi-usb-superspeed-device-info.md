---
title: EFI_USB_SUPERSPEED_DEVICE_INFO
description: EFI_USB_SUPERSPEED_DEVICE_INFO
ms.assetid: 7861BA16-7499-48A1-9D6A-9BB8F5AA36CE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2bcc9909d7cc666164b80e737d2b2b74f6afdb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563567"
---
# <a name="efiusbsuperspeeddeviceinfo"></a>EFI\_USB\_SUPERSPEED\_DEVICE\_INFO


**EFI\_USB\_SUPERSPEED\_设备\_信息**结构用于定义 USB SuperSpeed 函数设备。

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


<a href="" id="devicedescriptor"></a>**DeviceDescriptor**  
EFI\_USB\_设备\_描述符结构，其中包含 USB 设备的配置信息。

<a href="" id="configinfotable"></a>**ConfigInfoTable**  
[EFI\_USB\_SUPERSPEED\_CONFIG\_信息](efi-usb-superspeed-config-info.md)结构，其中包含有关所支持的 USB SuperSpeed 配置信息。

<a href="" id="bosdescriptor"></a>**BosDescriptor**  
[EFI\_USB\_BOS\_描述符](efi-usb-bos-descriptor.md)结构，其中包含有关二进制对象存储到 USB 功能驱动程序的信息。

## <a name="remarks"></a>备注


**EFI\_USB\_CONFIG\_描述符**结构是定义中的 UEFI 规范版本 2.3 及更高版本。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




