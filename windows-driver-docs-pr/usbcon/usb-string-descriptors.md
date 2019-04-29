---
Description: 设备、 配置和接口描述符可能包含对字符串描述符的引用。 本主题介绍如何从设备获取特定字符串描述符。
title: USB 字符串描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a899061b7910dd9149eb2c68c5bb156ee8b6f1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377199"
---
# <a name="usb-string-descriptors"></a>USB 字符串描述符


设备、 配置和接口描述符可能包含对字符串描述符的引用。 本主题介绍如何从设备获取特定字符串描述符。




按其基于 1 的索引号引用字符串描述符。 字符串描述符包含一个或多个 Unicode 字符串;每个字符串都转换其他为另一种语言。

客户端驱动程序使用[ **UsbBuildGetDescriptorRequest**](https://msdn.microsoft.com/library/windows/hardware/ff538943)，与*DescriptorType* = USB\_字符串\_描述符\_类型若要生成请求以获取字符串描述符。 *索引*参数指定的索引数目，并*LanguageID*参数指定的语言 ID （如 Microsoft Win32 LANGID 值中所示使用相同的值）。 驱动程序可以请求特殊索引数为零，则确定哪种语言 Id 设备支持。 对于此特殊值，设备将恢复的语言 Id 数组而不是 Unicode 字符串。

因为字符串描述符包含的可变长度数据，该驱动程序必须获取它在两个步骤。 该驱动程序必须首先发出请求，并传递数据缓冲区足够大以保存字符串描述符，USB 的标头\_字符串\_描述符结构。 **BLength** USB 成员\_字符串\_描述符指定的大小以字节为单位的整个描述符。 驱动程序，然后可以使用数据缓冲区的大小相同的请求**bLength**。

下面的代码演示如何请求*我*阶字符串描述符，语言 id *langID*:

```cpp
USB_STRING_DESCRIPTOR USD, *pFullUSD;
UsbBuildGetDescriptorRequest(
    pURB, // points to the URB to be filled in
    sizeof(struct _URB_CONTROL_DESCRIPTOR_REQUEST),
    USB_STRING_DESCRIPTOR_TYPE,
    i, // index of string descriptor
    langID, // language ID of string.
    &USD, // points to a USB_STRING_DESCRIPTOR.
    NULL,
    sizeof(USB_STRING_DESCRIPTOR),
    NULL
);
pFullUSD = ExAllocatePool(NonPagedPool, USD.bLength);
UsbBuildGetDescriptorRequest(
    pURB, // points to the URB to be filled in
    sizeof(struct _URB_CONTROL_DESCRIPTOR_REQUEST),
    USB_STRING_DESCRIPTOR_TYPE,
    i, // index of string descriptor
    langID, // language ID of string
    pFullUSD,
    NULL,
    USD.bLength,
    NULL
);
```

## <a name="related-topics"></a>相关主题
[USB 描述符](usb-descriptors.md)  



