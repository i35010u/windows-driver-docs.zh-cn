---
description: 设备、配置和接口描述符可能包含对字符串描述符的引用。 本主题介绍如何从设备获取特定字符串描述符。
title: USB 字符串描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8df18d32cffae9c25bca11aa0f4e98dbc44c10ac
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968594"
---
# <a name="usb-string-descriptors"></a>USB 字符串描述符


设备、配置和接口描述符可能包含对字符串描述符的引用。 本主题介绍如何从设备获取特定字符串描述符。




字符串描述符由其从1开始的索引号引用。 字符串描述符包含一个或多个 Unicode 字符串;每个字符串都是将其他字符串转换为另一种语言。

客户端驱动[**UsbBuildGetDescriptorRequest**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))程序使用具有*DescriptorType* = USB \_ 字符串 \_ 描述符类型的 UsbBuildGetDescriptorRequest， \_ 以生成获取字符串描述符的请求。 *Index*参数指定索引号， *LanguageID*参数指定语言 ID (相同的值在) 的 Microsoft Win32 LANGID 值中使用。 驱动程序可以请求0的特殊索引号，以确定设备支持的语言 Id。 对于此特殊值，设备将返回语言 Id 的数组，而不是 Unicode 字符串。

由于字符串描述符包含可变长度数据，因此驱动程序必须通过两个步骤来获取它。 首先，驱动程序必须发出请求，传递一个足以容纳字符串描述符的标头的数据缓冲区，即一个 USB \_ 字符串 \_ 说明符结构。 USB **bLength**字符串描述符的 bLength \_ 成员 \_ 指定整个描述符的大小（以字节为单位）。 然后，该驱动程序将使用大小为 **bLength**的数据缓冲区进行相同的请求。

下面的代码演示如何请求带有语言 ID *langID*的第*i*个字符串描述符：

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



