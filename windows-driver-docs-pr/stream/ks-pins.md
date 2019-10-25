---
title: KS 引脚
description: KS 引脚
ms.assetid: 04d0d17b-c326-417d-b2e8-58b33420455a
keywords:
- 锁定 WDK 内核流式处理
- KS 引脚-关于 KS 引脚的音频流式处理
- KSPIN_DESCRIPTOR
- IRP 源 pin WDK 内核流式处理
- 数据源引脚 WDK 内核流式处理
- 固定连接 WDK 内核流式处理
- 内核流 WDK，pin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac1482676e18168223bc5b7765c8a74ccacac67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842506"
---
# <a name="ks-pins"></a>KS 引脚





微型驱动程序为要实例化的每种类型的 pin 提供[**KSPIN\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构。 Pin 描述符结构称为 pin 工厂。 每个 pin 工厂都可以实例化特定类型的一个或多个固定实例。 Pin 工厂包含几个数组，这些数组描述此描述符实例化的 pin 类型。

微型驱动程序指定一个或多个 KS 类别，此描述符创建的 pin 属于 KSPIN\_描述符的**类别**成员。 当生成筛选器关系图时，KS 使用类别来连接 pin 实例。 [**KSPROPERTY\_拓扑\_类别**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)"属性查询驱动程序支持的功能类别的数组。

微型驱动程序提供了一个 INF 文件，用于注册一个或多个 pin 设备名称。 在安装时，操作系统会将名称和相应的类别加载到系统注册表中。 然后，客户端可以通过这些设备名称进行创建文件调用来实例化 pin。

用户模式客户端将 Win32 函数[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)与设备的名称一起调用。 例如，" *\\\\。\\筛选器\\音频\\默认呈现器*"可能是指向已为默认输出配置的音频设备的链接。 内核模式客户端从内核模式调用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile) 。 创建文件例程返回文件句柄后，KS 客户端通过[KS 属性](ks-properties.md)与 pin 实例通信。

在固定描述符结构中，微型驱动程序将[**KSPIN\_INTERFACE**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))结构和[**KSPIN\_MEDIUM**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))结构的数组，这些结构指定该 pin 工厂支持的[接口](ks-interfaces.md)和[媒体](ks-mediums.md)。 [**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)也是微型驱动程序为该工厂创建的 pin 指定有效数据范围的位置。 它通过提供指向[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构数组的指针来实现此功能。 微型驱动程序还指定此 pin 工厂创建的新 pin 的数据和通信流向。

微型驱动程序通过支持[KSPROPSETID\_固定](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)属性集来启用 pin 工厂的运行时发现。

若要创建 pin 连接，请调用[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)例程。 在此调用中，微型驱动程序将指针传递到 KSPIN 类型的结构[ **\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)，该结构描述请求的连接。 创建 pin 后，筛选器会将新的 pin 视为该筛选器的文件对象的文件对象。

微型驱动程序调用[**KsValidateConnectRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksvalidateconnectrequest) ，生成的 IRP\_MJ\_CREATE 中提供的描述符结构。 此例程验证这些结构并返回指向连接结构和根文件对象的指针。

微型驱动程序使用[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构的**数据流**和**通信**成员来定义以下 pin 说明：

-   **IRP 源 pin 与 IRP 接收器 pin**

    *Irp 源*pin 颁发了 irp;*IRP 接收器*pin 会接收它们。 用户模式客户端通过相关文件句柄直接向 IRP 接收器 pin 发送 i/o 请求。 客户端使用[**KSPROPERTY\_固定\_通信**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-communication)，以检查数据流入或流出 PIN 类型。

-   **数据源 pin 与数据接收器 pin**

    *数据源*pin 是筛选器上的输出插针;*数据接收器*pin 是一种输入插针。 作为数据源或接收器的属性独立于是 IRP 源或接收器。 例如，客户端可以连接数据源、IRP 接收器固定到数据接收器、IRP 源 pin。 客户端使用[**KSPROPERTY\_固定\_数据流**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataflow)来检查数据流是流入还是流出 PIN 类型。

在终止连接时，必须先关闭源 pin 的句柄，然后才能销毁基础文件对象。 如果源 pin 依赖于接收器 pin 提供的资源，则接收器 pin 负责在连接终止时通知源。

客户端通过使用[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)来调用**DeviceIoControl**例程（Microsoft Windows SDK 文档中所述）与内核流式处理 pin 交互。 调用方通过它放在 i/o 堆栈位置结构中的**DeviceIoControl IoControlCode**的 i/o 控制代码来标识其请求。

为了支持请求，微型驱动程序在对[**KsAllocateObjectHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksallocateobjectheader)的调用中提供了指向[**KSDISPATCH\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdispatch_table)结构的指针。

写入请求包含指向 KSSTREAM 数组的指针[ **\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构，后者又包含指向流数据的指针。 Read 请求包含一个指针，该指针指向应返回读取数据的空标头结构的数组。

 

 




