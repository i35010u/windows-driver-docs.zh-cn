---
title: 初始化 AVStream 微型驱动程序
description: 初始化 AVStream 微型驱动程序
keywords:
- AVStream WDK，初始化微型驱动程序
- 微型驱动程序 WDK AVStream，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bd1cd5dc17b86c8cdc1f50810d58ec5faab169f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790271"
---
# <a name="initializing-an-avstream-minidriver"></a>初始化 AVStream 微型驱动程序





AVStream 微型驱动程序，它不会在其自己的调用 [**KsInitializeDriver**](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) 上处理来自微型驱动程序的 [**DriverEntry**](/previous-versions/ff554081(v=vs.85)) 例程的设备初始化。 除了 IRP 调度、PnP 添加设备消息和卸载外， **KsInitializeDriver** 还初始化 AVStream 驱动程序的驱动程序对象。

在调用 **KsInitializeDriver** 时，微型驱动程序将传递指向驱动程序对象的指针，以初始化指向注册表路径的指针，还可以选择使用设备描述符对象。 请注意，不需要传递 [**KSDEVICE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor) 对象。 如果微型驱动程序传递了一个设备描述符，则 AVStream 将在 AddDevice 时间创建具有指定特征的设备。

设备描述符对象包含指向 [**KSDEVICE \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch) 结构以及筛选器描述符数组的指针。 为微型驱动程序支持的每个筛选器类型提供 [**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor) 。 当微型驱动程序调用 [**KsInitializeDriver**](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)时，AVStream 将为微型驱动程序公开的每种类型的筛选器创建一个筛选器工厂对象。 然后，筛选器工厂会在为关联的创建项接收 create IRP 时实例化单个筛选器。 每个筛选器描述符都包含指向 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) 对象的数组的指针。 AVStream 为微型驱动程序通过该筛选器公开的每种类型的 pin，在相关的筛选器上创建一个 pin 工厂。

在筛选器上建立到给定的 pin 类型的连接时，AVStream pin 工厂会创建一个 pin 对象。 请注意，每个筛选器必须公开至少一个 pin。 微型驱动程序使用 KSPIN 描述符的 **InstancesNecessary** 成员（ \_ \_ 例如）标识筛选器正常运行所需的此类型的实例的数目。 同样，微型驱动程序可以使用此结构的 **InstancesPossible** 成员对 pin 工厂可以实例化的 pin 量进行最大限制。

AVStream 支持两种处理类型：以 [筛选为中心的处理](filter-centric-processing.md)和以 [针为中心的处理](pin-centric-processing.md)。 布局描述符时，确定每个筛选器类型将执行哪种类型的处理。

### <a name="installing-an-avstream-minidriver"></a>安装 AVStream 微型驱动程序

AVStream 微型驱动程序必须具有系统用于安装驱动程序的 INF 文件。 AVStream INF 文件基于常见 INF 格式，如 [创建 INF 文件](../install/overview-of-inf-files.md)中所述。 你还可以参阅 Windows 驱动程序工具包 (WDK) 中提供的 AVStream 示例驱动程序的 INF 文件。 请记住以下 AVStream 特定的准则。

如果要为父设备编写微型驱动程序，则 INF 文件的 **AddReg** 部分应包含：

```INF
[ParentName.AddReg]
HKR,"ENUM\[DeviceName]",pnpid,,"[string]"
```

如果要为子设备编写微型驱动程序，则 **AddReg** 部分应包含：

```INF
[Manufacturer]
...=ChildName
[ChildName]
...=ChildName.Device,AVStream\[string]
```

请注意，对于 Stream 类驱动程序，"AVStream" 将为 "Stream"。

对于所有 AVStream 微型驱动程序，INF 文件中特定于筛选器的引用字符串必须与 [**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的 **ReferenceGuid** 成员匹配。

有关描述符的详细信息，请参阅 [AVStream 描述符](avstream-descriptors.md)。
