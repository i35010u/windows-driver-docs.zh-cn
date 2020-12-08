---
title: EFI_USB_BOS_DESCRIPTOR
description: EFI_USB_BOS_DESCRIPTOR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbad448adc9d1f395f6c3e4967d70eae1b60658c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789077"
---
# <a name="efi_usb_bos_descriptor"></a>EFI \_ USB \_ BOS \_ 描述符


**EFI \_ usb \_ BOS \_ 描述符** 结构提供有关二进制对象存储 (BOS) 到 USB 函数驱动程序的信息。

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


<a href="" id="length"></a>**长短**  
描述符的大小。

<a href="" id="descriptortype"></a>**DescriptorType**  
BOS 描述符类型。

<a href="" id="totallength"></a>**TotalLength**  
此描述符及其所有子说明符的长度。

<a href="" id="numdevicecaps"></a>**NumDeviceCaps**  
BOS 中的单独设备功能描述符的数目。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




