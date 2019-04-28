---
title: EFI_USB_ENDPOINT_TYPE
description: EFI_USB_ENDPOINT_TYPE
ms.assetid: 5cdb0efc-2355-42e2-929b-df19257e35c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2b3a6ea6199962da8716c62d271676f999aa3b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337767"
---
# <a name="efiusbendpointtype"></a>EFI\_USB\_ENDPOINT\_TYPE


**EFI\_USB\_终结点\_类型**枚举包含用来指示终结点的类型的值。

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
等时 transfe-连续有保证的带宽和界定的延迟的时间敏感数据的流。

<a href="" id="usbendpointbulk"></a>**UsbEndpointBulk**  
大容量传输-突发并且不能保证的带宽或最小延迟中的大量数据。

<a href="" id="usbendpointinterrupt"></a>**UsbEndpointInterrupt**  
中断传输-非定期通信的最大延迟保证。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




