---
title: 框架对象上下文空间
description: 框架对象上下文空间
ms.assetid: 21a46e04-2330-4a3d-ba72-c04295bfbb3c
keywords:
- framework 对象 WDK KMDF，上下文空间
- 上下文空间 WDK KMDF
- 对象上下文空间 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0462ec2c152cca8c51ff36625a57b80535555c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564898"
---
# <a name="framework-object-context-space"></a>框架对象上下文空间





*对象上下文空间*是额外，分页，驱动程序可以分配并分配到对象的内存空间。 每个基于 framework 的驱动程序可以创建为每个框架对象，该驱动程序接收或创建一个或多个特定于对象上下文空间。

基于框架的驱动程序应存储所有特定于对象的数据，通过值或指针，数据所属的对象的上下文空间中。

例如，USB 设备的驱动程序可能会创建其 framework 设备对象的上下文空间。 在上下文领域中，该驱动程序可能将此类特定于设备的信息存储为设备的[ **USB\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539280)并[ **USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)结构，加上的句柄[集合对象](framework-object-collections.md)，表示设备接口的管道。

框架不会传递 framework 对象从一个驱动程序到另一个，因此你无法使用对象的上下文空间以在两个驱动程序之间传递数据。

若要定义的对象上下文空间，必须创建一个或多个结构。 每个结构表示单独的上下文空间。 您的驱动程序将使用每个结构成员来存储一条特定于对象的信息。 此外，您的驱动程序必须让 framework 生成*访问器方法*为每个结构。 此访问器方法接受对象句柄作为输入并返回对象的上下文空间的地址。

每当您的驱动程序调用对象创建方法，如[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)，该方法根据需要分配上下文空间。 所有对象创建方法都接受一个可选[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构作为输入。 此结构描述你想要分配给该对象的框架的上下文空间。

若要向对象添加其他上下文空间，该驱动程序已调用对象的创建方法后，该驱动程序可以调用[ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)方法-例如对象创建方法接受[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构作为输入。

当框架分配的对象上下文空间时，它还执行零初始化上下文空间。

当框架或驱动程序删除 framework 对象时，该框架将删除所有对象的上下文空间。

如果您的驱动程序使用上下文空间来存储驱动程序时它会创建一个对象，该驱动程序应提供分配的缓冲区的指针[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)解除分配的函数删除对象时的缓冲区。

若要定义的对象上下文空间结构和驱动程序创建的对象的访问器方法，您的驱动程序必须使用以下步骤：

1.  定义用于描述您想要存储的数据结构。 例如，如果你想要创建驱动程序的设备对象的上下文数据，您的驱动程序可以定义称为 MY 的结构\_设备\_上下文。

2.  可以使用两种[ **WDF\_DECLARE\_上下文\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff551250)宏或[ **WDF\_DECLARE\_上下文\_类型\_WITH\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff551252)宏。 这两个这些宏执行以下操作：

    -   创建和初始化[ **WDF\_对象\_上下文\_类型\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff552407)结构。
    -   定义您的驱动程序将更高版本用于访问对象的上下文空间的访问器方法。 访问器方法的返回值是指向对象的上下文空间。

    WDF\_DECLARE\_上下文\_类型宏创建取值函数方法的名称中结构的名称。 例如，如果上下文结构的名称为 MY\_设备\_上下文中，宏会创建名为一个访问器方法**WdfObjectGet\_MY\_设备\_上下文**.

    WDF\_DECLARE\_上下文\_类型\_WITH\_名称宏，可以指定访问器方法的名称。 例如，可以指定**GetMyDeviceContext**作为设备对象上下文的访问器方法的名称。

3.  调用[ **WDF\_对象\_特性\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552402)初始化对象的[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构。

4.  使用[ **WDF\_对象\_特性\_设置\_上下文\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff552405)宏设置**ContextTypeInfo**隶属 WDF\_对象\_WDF 的地址的属性结构\_对象\_上下文\_类型\_信息结构。

5.  调用对象创建方法，如[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。

您的驱动程序已创建了对象后，该驱动程序可以调用[ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)在任何时间将更多上下文空间添加到对象。

步骤 1 和 2 定义的全局数据结构，并创建一个驱动程序可调用的例程，因为您的驱动程序必须完成这些步骤中声明全局数据--通常标头文件的驱动程序的区域。 驱动程序的例程中，必须完成从这些步骤。

您的驱动程序必须完成步骤 3、 4 和 5 从中将创建一个对象，例如一个驱动程序例程[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)调用的回调函数[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。

框架可创建两种类型的对象-framework 请求对象和框架文件对象--代表您的驱动程序。 您的驱动程序可以通过调用注册这些对象的上下文空间[ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)并[ **WdfDeviceInitSetFileObjectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff546107)分别。 您的驱动程序还可以调用[ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)分配这些对象的上下文空间。

创建对象后，该驱动程序可以使用以下方法之一获取指向对象的上下文空间：

-   调用通过使用前面的过程中的步骤 2 中创建的上下文访问器方法[ **WDF\_DECLARE\_上下文\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff551250)或[**WDF\_DECLARE\_上下文\_类型\_WITH\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff551252)宏。

-   调用[ **WdfObjectGetTypedContext**](https://msdn.microsoft.com/library/windows/hardware/ff548749)，提供的驱动程序定义的上下文结构的名称。

如果您的驱动程序具有上下文空间指针，它可以找到所属对象的上下文空间通过调用[ **WdfObjectContextGetObject**](https://msdn.microsoft.com/library/windows/hardware/ff548727)。

 

 





