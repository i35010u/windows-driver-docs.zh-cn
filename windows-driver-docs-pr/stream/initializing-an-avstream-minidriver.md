---
title: 初始化 AVStream 微型驱动程序
description: 初始化 AVStream 微型驱动程序
ms.assetid: 666d6efb-93ec-43f3-87c5-ea1a3983bfd0
keywords:
- AVStream WDK，初始化微型驱动程序
- 微型驱动程序 WDK AVStream 初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db50de85c55d68cc83f2dd8349601de078dd907b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360671"
---
# <a name="initializing-an-avstream-minidriver"></a>初始化 AVStream 微型驱动程序





不会处理在其自己的调用上的设备初始化 AVStream 微型驱动程序[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)微型驱动程序的从[ **DriverEntry**](https://docs.microsoft.com/previous-versions/ff554081(v=vs.85))例程。 **KsInitializeDriver**初始化 AVStream 驱动程序的驱动程序对象、 调度、 PnP IRP 除了添加设备的消息，并卸载。

在调用**KsInitializeDriver**，微型驱动程序将指针传递给要初始化的指针到注册表路径的驱动程序对象和 （可选），设备描述符对象。 请注意，传递[ **KSDEVICE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_descriptor)对象不需要。 如果设备描述符 pass 微型驱动程序，AVStream 创建的设备具有指定特征在 AddDevice 时。

设备描述符对象包含一个指向[ **KSDEVICE\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_dispatch)结构，以及数组的筛选器描述符。 提供[ **KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)你微型驱动程序支持每种筛选器类型。 当调用微型驱动程序[ **KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)，AVStream 创建每种类型的筛选器公开的微型驱动程序的筛选器工厂对象。 在收到创建 IRP 为关联的创建项时的筛选器工厂然后实例化单个筛选器。 每个筛选器描述符包含数组的指针[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)对象。 AVStream pin 微型驱动程序通过该筛选器公开的每种类型的相关筛选器上创建 pin 工厂。

在为给定的 pin 类型对筛选器建立连接，AVStream pin 工厂将创建一个 pin 对象。 请注意每个筛选器必须公开至少一个 pin。 微型驱动程序使用**InstancesNecessary** KSPIN 成员\_描述符\_EX 来标识所需的筛选器才能正确运行此 pin 类型的实例数。 同样，微型驱动程序造成的 pin 工厂可以实例化使用的 pin 数最多**InstancesPossible**此结构的成员。

AVStream 支持两种类型的处理：[筛选器以处理](filter-centric-processing.md)，并[pin 以中心处理](pin-centric-processing.md)。 当布局描述符，确定将执行哪种类型的处理每个筛选器类型。

### <a name="installing-an-avstream-minidriver"></a>安装 AVStream 微型驱动程序

AVStream 微型驱动程序必须具有系统使用安装驱动程序的 INF 文件。 AVStream INF 文件基于常见的 INF 格式中所述[创建一个 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)。 您还可以参考提供与 AVStream 示例驱动程序在 Windows Driver Kit (WDK) 的 INF 文件。 请注意以下特定于 AVStream 的指导原则。

如果你正在编写父设备，微型驱动程序**AddReg** INF 文件的部分应包含：

```INF
[ParentName.AddReg]
HKR,"ENUM\[DeviceName]",pnpid,,"[string]"
```

如果你正在编写子设备，微型驱动程序**AddReg**部分应包含：

```INF
[Manufacturer]
...=ChildName
[ChildName]
...=ChildName.Device,AVStream\[string]
```

请注意该"AVStream"的流类驱动程序将"Stream"。

对于所有 AVStream 微型驱动程序，INF 文件中的特定于筛选器的引用字符串必须匹配**ReferenceGuid**的成员[ **KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)结构。

有关描述符的详细信息，请参阅[AVStream 描述符](avstream-descriptors.md)。
