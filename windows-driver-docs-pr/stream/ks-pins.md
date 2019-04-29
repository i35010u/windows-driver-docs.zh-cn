---
title: KS 引脚
description: KS 引脚
ms.assetid: 04d0d17b-c326-417d-b2e8-58b33420455a
keywords:
- pin WDK 内核流式处理
- 流式处理，有关 KS pin KS pin WDK 内核
- KSPIN_DESCRIPTOR
- 流式处理 IRP 源 pin WDK 内核
- 流式处理的数据源的 pin WDK 内核
- 将固定连接 WDK 内核的流式处理
- 流式处理 WDK，pin 的内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33065b11f048d781b815f8d6add44bf08889018
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380117"
---
# <a name="ks-pins"></a>KS 引脚





微型驱动程序提供[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)每种类型的 pin 以进行实例化的结构。 Pin 描述符结构称为固定工厂。 每个 pin 工厂可以实例化特定类型的一个或多个 pin 实例。 Pin 工厂包含描述此描述符实例化的 pin 的类型的多个数组。

微型驱动程序指定为创建此说明符的插针属于中的一个或多个 KS 类别**类别**KSPIN 成员\_描述符。 KS 使用类别来生成筛选器关系图时将 pin 实例的连接。 [ **KSPROPERTY\_拓扑\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff565799)属性查询数组的驱动程序支持的功能类别。

微型驱动程序提供了一个 INF 文件注册一个或多个插针设备名称。 安装时，操作系统将加载的名称和相应类别到系统注册表。 客户端然后可以使用这些设备名称的创建文件调用来实例化的 pin。

用户模式下客户端调用 Win32 函数[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)与设备的名称。 例如，"*\\\\。\\筛选器\\音频\\默认呈现器*"可能是已配置为默认输出的音频设备的链接。 内核模式下客户端调用[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)从内核模式。 创建文件例程将返回的文件句柄后，KS 客户端通信通过 pin 实例，并用[KS 属性](ks-properties.md)。

在 pin 描述符结构，微型驱动程序进行布局的数组[ **KSPIN\_界面**](https://msdn.microsoft.com/library/windows/hardware/ff563537)结构并[ **KSPIN\_中等**](https://msdn.microsoft.com/library/windows/hardware/ff563538)指定的结构[接口](ks-interfaces.md)并[媒介](ks-mediums.md)该 pin 工厂所支持的。 [**KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)也是其中微型驱动程序指定由该工厂创建的 pin 的有效的数据范围。 这是通过提供指向数组的指针[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构。 微型驱动程序还指定此 pin 工厂创建的新 pin 的数据和通信流的方向。

微型驱动程序通过支持启用允许 pin 工厂的运行时发现[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)属性集。

若要创建插针连接，请调用[ **KsCreatePin** ](https://msdn.microsoft.com/library/windows/hardware/ff561652)例程。 在此调用中，微型驱动程序将指针传递到类型的结构[ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531)描述请求的连接。 创建 pin 后，该筛选器会将新的 pin 视为属于该筛选器的文件对象的文件对象。

微型驱动程序调用[ **KsValidateConnectRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff567227)使用生成的 IRP 中提供的描述符结构\_MJ\_创建。 此例程验证这些结构，并返回指向的连接结构和根文件对象的指针。

微型驱动程序使用**数据流**并**通信**的成员[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)结构定义pin 具体如下：

-   **与 IRP 接收器 pin IRP 源 pin**

    *IRP 源*pin 发出 Irp; *IRP 接收器*pin 接收它们。 用户模式下客户端发送的 I/O 请求直接通过此相关的文件句柄的 IRP 接收器 pin。 客户端使用[ **KSPROPERTY\_PIN\_通信**](https://msdn.microsoft.com/library/windows/hardware/ff565194)检查数据是否流动加入或退出 pin 类型。

-   **数据源与数据接收器 pin 的 pin**

    一个*数据源*pin 是对筛选器; 输出插针*数据接收器*pin 是输入的 pin。 独立于正在的 IRP 源或接收器的数据源或接收器的属性。 例如，客户端可以连接数据源，IRP 接收器固定到的数据接收器，IRP 源 pin。 客户端使用[ **KSPROPERTY\_PIN\_数据流**](https://msdn.microsoft.com/library/windows/hardware/ff565197)检查数据是否流动加入或退出 pin 类型。

当终止连接，基础文件对象被销毁之前，必须关闭源 pin 的句柄。 如果源 pin 依赖于由接收器 pin 提供的资源，则接收器 pin，以在连接终止时通知源的责任。

客户端进行交互使用通过调用流 pin 内核**DeviceIoControl**例程 （Microsoft Windows SDK 文档中所述） 与[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)。 调用方标识的 I/O 控制代码，它会将放置在其请求**Parameters.DeviceIoControl.IoControlCode**中 I/O 堆栈位置结构。

若要支持请求，微型驱动程序提供一个指向[ **KSDISPATCH\_表**](https://msdn.microsoft.com/library/windows/hardware/ff561723)结构在调用[ **KsAllocateObjectHeader**](https://msdn.microsoft.com/library/windows/hardware/ff560972).

写入请求包含指向的数组的指针[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)又包含指向流数据的指针的结构。 读取请求包含指向空标头结构应返回读取的数据的位置的数组的指针。

 

 




