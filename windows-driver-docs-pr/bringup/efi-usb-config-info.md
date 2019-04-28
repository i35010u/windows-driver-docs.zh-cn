---
title: EFI_USB_CONFIG_INFO
description: EFI_USB_CONFIG_INFO
ms.assetid: 74d5cb02-2648-4bd1-990e-61156b5dc8cd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7db5cab0dc38e26f692b13f69f52e47c277ec9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337786"
---
# <a name="efiusbconfiginfo"></a>EFI\_USB\_CONFIG\_信息


**EFI\_USB\_CONFIG\_信息**结构用于定义受支持的 USB 端口配置。

## <a name="syntax"></a>语法


```cpp
typedef struct 
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_INTERFACE_INFO              **InterfaceInfoTable;
} EFI_USB_CONFIG_INFO;
```

## <a name="members"></a>成员


<a href="" id="configdescriptor"></a>**ConfigDescriptor**  
EFI\_USB\_CONFIG\_描述符结构，其中包含 USB 函数设备的配置信息。

<a href="" id="interfaceinfotable"></a>**InterfaceInfoTable**  
[EFI\_USB\_界面\_信息](efi-usb-interface-info.md)结构，其中包含有关受支持的接口的信息。

## <a name="remarks"></a>备注


结构**USB\_CONFIG\_描述符**UEFI 规范 2.3 中定义。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




