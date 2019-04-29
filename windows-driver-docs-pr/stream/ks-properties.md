---
title: KS 属性
description: KS 属性
ms.assetid: a385929e-1934-4d88-aaf9-ff1ddbfd30f7
keywords:
- 内核流式处理 WDK，属性
- KS 属性 WDK 内核流式处理
- 流式处理的属性 WDK 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 932ec700da1c63910b189d22f825ff0b748cd2a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382527"
---
# <a name="ks-properties"></a>KS 属性





一个*属性*表示属于流式处理的对象，如筛选器或 pin 的内核的功能或控件状态设置。 流式处理微型驱动程序的内核的客户端可以发送 get 并设置属性的请求 (KSPROPERTY\_类型\_GET 和 KSPROPERTY\_类型\_设置) 与筛选器和微型驱动程序已实例化的 pin。 一组相关属性被称为*属性集*。

若要获取或设置单独的属性，用户模式下客户端调用 Win32 函数**DeviceIoControl**与*dwIoControlCode*参数设置为 IOCTL\_KS\_属性。 **DeviceIoControl** Microsoft Windows SDK 文档中所述。 内核模式下客户端应调用[ **KsSynchronousDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/ff567142)。

输入的缓冲区是[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)结构或包含 KSPROPERTY 结构和其他信息与请求相关的包装器。 以响应此调用，操作系统将调度到的类驱动程序 IRP。

当在类驱动程序收到生成 IRP 时，它将调用[ **KsPropertyHandler**](https://msdn.microsoft.com/library/windows/hardware/ff564263)。 在类驱动程序作为调用参数包括标识属性请求的具体情况 KSPROPERTY 结构的地址。 属性请求是可以自动处理类驱动程序级别或微型驱动程序提供处理程序。 请参阅[内核流式处理属性设置](https://msdn.microsoft.com/library/windows/hardware/ff554246)的参考信息，包括由类驱动程序处理的属性集，这需要提供微型驱动程序的处理程序。 微型驱动程序可以覆盖或扩充通过提供回调是默认情况下由类驱动程序处理的属性的类驱动程序处理程序。

如果微型驱动程序已为此属性，提供处理程序**KsPropertyHandler**反过来移交到合适的微型驱动程序提供回调请求。

微型驱动程序提供了指向其类型的结构中的属性支持回调[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)。 微型驱动程序组的相关 KSPROPERTY 数组\_结构中的项[ **KSPROPERTY\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff565617)结构。 不同的类驱动程序模型具有微型驱动程序以使属性设置为类驱动程序的可用数据的方法稍有不同。 可以按照中的链接查找类特定于驱动程序信息[内核流式处理](kernel-streaming.md)。

微型驱动程序还提供了一个指向[ **KSPROPERTY\_值**](https://msdn.microsoft.com/library/windows/hardware/ff565966) KSPROPERTY 中的结构\_项结构。 KSPROPERTY\_值结构又包含一个数组[ **KSPROPERTY\_MEMBERSLIST** ](https://msdn.microsoft.com/library/windows/hardware/ff565190)结构。 这是其中微型驱动程序指定的大小和类型的属性可接受的值。 每个 KSPROPERTY\_MEMBERSLIST 结构包含一个标头： 请参阅[ **KSPROPERTY\_MEMBERSHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff565189)有关如何指定合法范围或值的信息将微型驱动程序支持的属性。 此外可以找到此机制中的实现*Testcap*中 Microsoft Windows Driver Kit (WDK) 示例。

若要报告的大小和类型的属性可接受的值，在类驱动程序返回[ **KSPROPERTY\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff565132) KSPROPERTY 响应结构\_类型\_BASICSUPPORT 请求从客户端。

在类驱动程序可能会追加一系列 KSPROPERTY\_KSPROPERTY MEMBERSHEADER 结构\_描述结构。

 

 




