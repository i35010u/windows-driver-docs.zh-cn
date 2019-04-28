---
title: EFI_USB_BOS_DESCRIPTOR
description: EFI_USB_BOS_DESCRIPTOR
ms.assetid: A12E3678-E5B6-4AB0-8F28-FCDA57C9D397
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb849b3b17e57852134e697e4a50d798bea5b11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337756"
---
# <a name="efiusbbosdescriptor"></a>EFI\_USB\_BOS\_描述符


**EFI\_USB\_BOS\_描述符**结构提供了有关 USB 函数驱动程序的对象二进制存储区 (BOS) 的信息。

## <a name="syntax"></a>语法


```cpp
typedef struct
{
    UINT8   Length;
    UINT8   DescriptorType;
    UINT16  TotalLength;
    UINT8   NumDeviceCaps;
} EFI_USB_BOS_DESCRIPTOR;
```

## <a name="members"></a>成员


<a href="" id="length"></a>**长度**  
描述符的大小。

<a href="" id="descriptortype"></a>**DescriptorType**  
BOS 描述符类型。

<a href="" id="totallength"></a>**TotalLength**  
此说明符和的所有子描述符的长度。

<a href="" id="numdevicecaps"></a>**NumDeviceCaps**  
BOS 中的单独的设备功能说明符的数目。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




