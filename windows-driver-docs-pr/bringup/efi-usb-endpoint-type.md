---
title: EFI_USB_ENDPOINT_TYPE
description: EFI_USB_ENDPOINT_TYPE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24d87613d8d7d138acf4a821e99cc9299a3d1902
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789073"
---
# <a name="efi_usb_endpoint_type"></a>EFI \_ USB \_ 终结点 \_ 类型


**EFI \_ USB \_ 终结点 \_ 类型** 枚举包含用来指示终结点类型的值。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USB_ENDPOINT_TYPE{
  UsbEndpointControl = 0x00,
  UsbEndpointIsochronous = 0x01,
  UsbEndpointBulk = 0x02,
  UsbEndpointInterrupt = 0x03
} EFI_USB_ENDPOINT_TYPE;
```

## <a name="constants"></a>常量


<a href="" id="usbendpointcontrol"></a>**UsbEndpointControl**  
控制传输-命令和状态操作。

<a href="" id="usbendpointisochronous"></a>**UsbEndpointIsochronous**  
同步 transfe-具有有保证带宽和有限延迟的时间敏感数据的连续流。

<a href="" id="usbendpointbulk"></a>**UsbEndpointBulk**  
大容量传输-突发的大量数据，不保证带宽或最小滞后时间。

<a href="" id="usbendpointinterrupt"></a>**UsbEndpointInterrupt**  
中断传输-不定期通信，保证最大延迟。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




