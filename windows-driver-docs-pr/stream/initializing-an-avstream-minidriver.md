---
title: 初始化 AVStream 微型驱动程序
description: 初始化 AVStream 微型驱动程序
ms.assetid: 666d6efb-93ec-43f3-87c5-ea1a3983bfd0
keywords:
- AVStream WDK，初始化微型驱动程序
- 微型驱动程序 WDK AVStream，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44f6c78e8e089e36feb9c5f94e8d74c1ea5ca307
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845570"
---
# <a name="initializing-an-avstream-minidriver"></a>初始化 AVStream 微型驱动程序





AVStream 微型驱动程序，它不会在其自己的调用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)上处理来自微型驱动程序的[**DriverEntry**](https://docs.microsoft.com/previous-versions/ff554081(v=vs.85))例程的设备初始化。 除了 IRP 调度、PnP 添加设备消息和卸载外， **KsInitializeDriver**还初始化 AVStream 驱动程序的驱动程序对象。

在调用**KsInitializeDriver**时，微型驱动程序将传递指向驱动程序对象的指针，以初始化指向注册表路径的指针，还可以选择使用设备描述符对象。 请注意，不需要传递[**KSDEVICE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)对象。 如果微型驱动程序传递了一个设备描述符，则 AVStream 将在 AddDevice 时间创建具有指定特征的设备。

设备描述符对象包含指向[**KSDEVICE\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch)结构以及筛选器描述符数组的指针。 为微型驱动程序支持的每种筛选器类型提供[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)。 当微型驱动程序调用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)时，AVStream 将为微型驱动程序公开的每种类型的筛选器创建一个筛选器工厂对象。 然后，筛选器工厂会在为关联的创建项接收 create IRP 时实例化单个筛选器。 每个筛选器描述符都包含指向 KSPIN 的数组的指针[ **\_EX 对象\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)。 AVStream 为微型驱动程序通过该筛选器公开的每种类型的 pin，在相关的筛选器上创建一个 pin 工厂。

在筛选器上建立到给定的 pin 类型的连接时，AVStream pin 工厂会创建一个 pin 对象。 请注意，每个筛选器必须公开至少一个 pin。 微型驱动程序使用 KSPIN\_描述符\_的**InstancesNecessary**成员来标识此类型的实例的数目，筛选器需要这些实例才能正常运行。 同样，微型驱动程序可以使用此结构的**InstancesPossible**成员对 pin 工厂可以实例化的 pin 量进行最大限制。

AVStream 支持两种处理类型：以[筛选为中心的处理](filter-centric-processing.md)和以[针为中心的处理](pin-centric-processing.md)。 布局描述符时，确定每个筛选器类型将执行哪种类型的处理。

### <a name="installing-an-avstream-minidriver"></a>安装 AVStream 微型驱动程序

AVStream 微型驱动程序必须具有系统用于安装驱动程序的 INF 文件。 AVStream INF 文件基于常见 INF 格式，如[创建 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)中所述。 你还可以参阅 Windows 驱动程序工具包（WDK）中随 AVStream 示例驱动程序提供的 INF 文件。 请记住以下 AVStream 特定的准则。

如果要为父设备编写微型驱动程序，则 INF 文件的**AddReg**部分应包含：

```INF
[ParentName.AddReg]
HKR,"ENUM\[DeviceName]",pnpid,,"[string]"
```

如果要为子设备编写微型驱动程序，则**AddReg**部分应包含：

```INF
[Manufacturer]
...=ChildName
[ChildName]
...=ChildName.Device,AVStream\[string]
```

请注意，对于 Stream 类驱动程序，"AVStream" 将为 "Stream"。

对于所有 AVStream 微型驱动程序，INF 文件中特定于筛选器的引用字符串必须与[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的**ReferenceGuid**成员匹配。

有关描述符的详细信息，请参阅[AVStream 描述符](avstream-descriptors.md)。
