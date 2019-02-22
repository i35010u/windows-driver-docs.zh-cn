---
title: EFI_USB_INTERFACE_INFO
description: EFI_USB_INTERFACE_INFO
ms.assetid: d20b78bd-8369-4f50-b161-e8ad0bb4c52f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8af735b385de3b47075f1eebf938a2129c902991
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546705"
---
# <a name="efiusbinterfaceinfo"></a>EFI\_USB\_INTERFACE\_INFO


**EFI\_USB\_界面\_信息**结构，用于定义支持的 USB 接口。

## <a name="syntax"></a>语法


```cpp
typedef struct 
{
    EFI_USB_INTERFACE_DESCRIPTOR        *InterfaceDescriptor;
    EFI_USB_ENDPOINT_DESCRIPTOR         **EndpointDescriptorTable;
} EFI_USB_INTERFACE_INFO;
```

## <a name="members"></a>成员


<a href="" id="interfacedescriptor"></a>**InterfaceDescriptor**  
EFI\_USB\_接口\_描述符结构，其中包含有关 USB 函数接口的信息。 请参阅**备注**。

<a href="" id="endpointdescriptortable"></a>**EndpointDescriptorTable**  
EFI\_USB\_终结点\_描述符结构，其中包含有关受支持的端点的信息。 请参阅**备注**。

## <a name="remarks"></a>备注


**USB\_界面\_描述符**并**USB\_终结点\_描述符**UEFI 规范 2.3 中定义结构。 有关详细信息，请访问[UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526)网站。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




