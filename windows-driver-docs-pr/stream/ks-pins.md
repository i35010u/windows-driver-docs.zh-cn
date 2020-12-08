---
title: KS 引脚
description: KS 引脚
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
ms.openlocfilehash: 94977535cc552cbf70ba1d308bb0a6fc66307760
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837075"
---
# <a name="ks-pins"></a>KS 引脚





微型驱动程序为要实例化的每种类型的 pin 提供 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 结构。 Pin 描述符结构称为 pin 工厂。 每个 pin 工厂都可以实例化特定类型的一个或多个固定实例。 Pin 工厂包含几个数组，这些数组描述此描述符实例化的 pin 类型。

微型驱动程序指定一个或多个 KS 类别，此描述符创建的 pin 属于 KSPIN 描述符的 **类别** 成员 \_ 。 当生成筛选器关系图时，KS 使用类别来连接 pin 实例。 [**KSPROPERTY \_ 拓扑 \_ 类别**](./ksproperty-topology-categories.md)属性用于查询驱动程序支持的功能类别的数组。

微型驱动程序提供了一个 INF 文件，用于注册一个或多个 pin 设备名称。 在安装时，操作系统会将名称和相应的类别加载到系统注册表中。 然后，客户端可以通过这些设备名称进行创建文件调用来实例化 pin。

用户模式客户端将 Win32 函数 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 与设备的名称一起调用。 例如，"*\\ \\ 。 \\筛选 \\ 音频 \\ 默认呈现器*"可以是已为默认输出配置的音频设备的链接。 内核模式客户端从内核模式调用 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile) 。 创建文件例程返回文件句柄后，KS 客户端通过 [KS 属性](ks-properties.md)与 pin 实例通信。

在固定描述符结构中，微型驱动程序将对 [**KSPIN \_ 接口**](/previous-versions/ff563537(v=vs.85)) 结构和 [**KSPIN \_ MEDIUM**](/previous-versions/ff563538(v=vs.85)) 结构的数组进行布局，这些结构指定该 pin 工厂支持的 [接口](ks-interfaces.md) 和 [媒体](ks-mediums.md) 。 [**KSPIN \_描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 也是微型驱动程序为该工厂创建的 pin 指定有效数据范围的位置。 它通过提供指向 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构数组的指针来实现此功能。 微型驱动程序还指定此 pin 工厂创建的新 pin 的数据和通信流向。

微型驱动程序通过支持 [KSPROPSETID \_ pin](./kspropsetid-pin.md) 属性集来启用 pin 工厂的运行时发现。

若要创建 pin 连接，请调用 [**KsCreatePin**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin) 例程。 在此调用中，微型驱动程序将传递指向描述所请求连接的 [**KSPIN \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect) 类型的结构的指针。 创建 pin 后，筛选器会将新的 pin 视为该筛选器的文件对象的文件对象。

微型驱动程序调用 [**KsValidateConnectRequest**](/windows-hardware/drivers/ddi/ks/nf-ks-ksvalidateconnectrequest) ，生成的 IRP MJ CREATE 中提供了描述符 \_ 结构 \_ 。 此例程验证这些结构并返回指向连接结构和根文件对象的指针。

微型驱动程序使用 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构的 **数据流** 和 **通信** 成员来定义以下 pin 具体内容：

-   **IRP 源 pin 与 IRP 接收器 pin**

    *Irp 源* pin 颁发了 irp;*IRP 接收器* pin 会接收它们。 用户模式客户端通过相关文件句柄直接向 IRP 接收器 pin 发送 i/o 请求。 客户端使用 [**KSPROPERTY 的 \_ pin \_ 通信**](./ksproperty-pin-communication.md) 来检查数据流入或流出 pin 类型。

-   **数据源 pin 与数据接收器 pin**

    *数据源* pin 是筛选器上的输出插针;*数据接收器* pin 是一种输入插针。 作为数据源或接收器的属性独立于是 IRP 源或接收器。 例如，客户端可以连接数据源、IRP 接收器固定到数据接收器、IRP 源 pin。 客户端使用 [**KSPROPERTY 的 \_ pin \_ 数据流**](./ksproperty-pin-dataflow.md) 来检查数据流是流入还是流出 pin 类型。

在终止连接时，必须先关闭源 pin 的句柄，然后才能销毁基础文件对象。 如果源 pin 依赖于接收器 pin 提供的资源，则接收器 pin 负责在连接终止时通知源。

客户端通过使用 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)) Microsoft Windows SDK 文档中所述的 **DeviceIoControl** (例程，与内核流式处理 pin 交互。 调用方通过它放在 i/o 堆栈位置结构中的 **DeviceIoControl IoControlCode** 的 i/o 控制代码来标识其请求。

为了支持请求，微型驱动程序在对 [**KsAllocateObjectHeader**](/windows-hardware/drivers/ddi/ks/nf-ks-ksallocateobjectheader)的调用中提供了指向 [**KSDISPATCH \_ 表**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdispatch_table)结构的指针。

写入请求包含指向 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header) 结构数组的指针，后者又包含指向流数据的指针。 Read 请求包含一个指针，该指针指向应返回读取数据的空标头结构的数组。

 

