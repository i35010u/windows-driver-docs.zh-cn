---
title: KS 属性
description: KS 属性
ms.assetid: a385929e-1934-4d88-aaf9-ff1ddbfd30f7
keywords:
- 内核流 WDK，属性
- KS 属性 WDK 内核流式处理
- 属性 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04e309da40564c44f859a9cdafdbef30ee015f90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842505"
---
# <a name="ks-properties"></a>KS 属性





*属性*表示属于内核流式处理对象（例如筛选器或 pin）的功能或控件状态设置。 内核流式处理微型驱动程序的客户端可以向微型驱动程序已经实例化的筛选器和 pin 发送 get 和 set 属性请求（KSPROPERTY\_类型\_GET 和 KSPROPERTY\_类型\_）。 一组相关属性称为*属性集*。

若要获取或设置单个属性，用户模式客户端将调用 Win32 函数**DeviceIoControl** ，并将*dwIoControlCode*参数设置为 IOCTL\_KS\_属性。 Microsoft Windows SDK 文档中介绍了**DeviceIoControl** 。 内核模式客户端应调用[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)。

输入缓冲区可以是[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)结构，也可以是包含 KSPROPERTY 结构和与请求相关的其他信息的包装。 为响应此调用，操作系统会将 IRP 调度到类驱动程序。

类驱动程序收到生成的 IRP 后，它将调用[**KsPropertyHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspropertyhandler)。 类驱动程序将 KSPROPERTY 结构的地址作为调用参数包括，该结构标识属性请求的细节。 属性请求在类驱动程序级别或由微型驱动程序提供的处理程序中自动处理。 有关参考信息，请参阅[内核流式处理属性集](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-property-sets)，其中包括类驱动程序处理哪些属性集以及需要微型驱动程序提供的处理程序。 微型驱动程序可以通过为默认情况下由类驱动程序处理的属性提供回调，来重写或增强类驱动程序处理程序。

如果微型驱动程序提供了此属性的处理程序，则**KsPropertyHandler**会将请求移交给适当微型驱动程序提供的回调。

微型驱动程序提供指向其属性的[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)类型的结构的指针支持回调。 微型驱动程序在[**KSPROPERTY\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构中对相关 KSPROPERTY\_项结构的数组进行分组。 不同的类驱动程序模型具有略微不同的方法，使微型驱动程序可以向类驱动程序提供属性集数据。 可以按照[内核流](kernel-streaming.md)中的链接查找特定于类驱动程序的信息。

微型驱动程序还提供了一个指针，指向 KSPROPERTY\_项结构中的[**KSPROPERTY\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_values)结构。 KSPROPERTY\_值结构又包含[**KSPROPERTY\_MEMBERSLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist)结构的数组。 这是微型驱动程序为属性指定可接受值的大小和类型的位置。 每个 KSPROPERTY\_MEMBERSLIST 结构都包含一个标头成员：有关如何为微型驱动程序支持的属性指定合法范围或值的信息，请参阅[**KSPROPERTY\_MEMBERSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader) 。 你还可以在 Microsoft Windows 驱动程序工具包（WDK）中的*Testcap*示例中找到此机制的实现。

为了报告属性的可接受值的大小和类型，类驱动程序将返回[**KSPROPERTY\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description)结构，以响应 KSPROPERTY\_类型\_BASICSUPPORT 请求从客户端请求。

类驱动程序可以将 KSPROPERTY\_MEMBERSHEADER 结构的列表追加到 KSPROPERTY\_说明结构。

 

 




