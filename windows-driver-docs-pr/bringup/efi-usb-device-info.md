---
title: EFI_USB_DEVICE_INFO
description: EFI_USB_DEVICE_INFO
ms.assetid: b44f77fc-f496-488f-b53a-b54420da9360
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79fb8ed527c791ac5b5dcdeae77172ee4cd796e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337806"
---
# <a name="efiusbdeviceinfo"></a>EFI\_USB\_DEVICE\_INFO


**EFI\_USB\_设备\_信息**结构用于定义 USB 函数设备。

## <a name="syntax"></a>语法


```cpp
typedef struct 
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_CONFIG_INFO                 **ConfigInfoTable;
} EFI_USB_DEVICE_INFO;
```

## <a name="members"></a>成员


<a href="" id="devicedescriptor"></a>**DeviceDescriptor**  
EFI\_USB\_设备\_描述符结构，其中包含 USB 设备的配置信息。

<a href="" id="configinfotable"></a>**ConfigInfoTable**  
EFI\_USB\_CONFIG\_信息结构，其中包含有关所支持的配置信息。

## <a name="remarks"></a>备注


**EFI\_USB\_CONFIG\_描述符**并**EFI\_USB\_设备\_描述符**结构定义在 UEFI 规范 2.3。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




