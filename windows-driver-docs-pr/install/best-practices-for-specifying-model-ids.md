---
title: 指定模型 ID 的最佳做法
description: 指定模型 ID 的最佳做法
ms.assetid: ed0cdfb4-1de8-4b4f-8bab-7c5e06cf96f6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242e032b547c35560831e7859299d82987d34b83
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380319"
---
# <a name="best-practices-for-specifying-model-ids"></a>指定模型 ID 的最佳做法


模型 Id 基于物理设备的业务定义或股票保留单位 (SKU)。 每个模型 ID 必须是唯一的所有品牌和型号的物理设备。

以下列表描述了硬件 Id 和模型 Id。 对于物理设备之间的差异：

-   [硬件 Id](hardware-ids.md)通过使用一个或多个指定[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)内的 XML 元素[ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121) XML元素。 每个**HardwareID**值指定硬件函数基于特定于总线的值。 硬件 Id 可以用于将设备驱动程序映射到设备实例。

    例如，具有相同的硬件 ID 的两个设备共享相同的驱动程序使用的功能接口。

-   通过使用一个或多个指定模型 Id [ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)中的 XML 元素[ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303) XML 元素。 模型 Id 允许原始设备制造商 (OEM) 或独立硬件供应商 (IHV) 来唯一标识的总线或接口技术独立的物理设备。

    例如，具有不同的模型 Id 的两个设备可能有其组件的相同硬件 Id。

-   [硬件 Id](hardware-ids.md)用于将设备元数据包映射到特定的总线或接口上的设备实例。

-   模型 Id 用于将设备元数据包映射到物理设备，而不考虑如何将设备连接到计算机。

[ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303) XML 元素是必需的仅当[ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)元素中未指定[**PackageInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549574) XML 数据。 如果指定了它，则**ModelIDList**元素必须包含一个或多个[ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)元素，以指定每个设备支持的函数的唯一模型 ID。

如果[ **PackageInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549574) XML 数据包含[ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)并[ **ModelIDList**](https://msdn.microsoft.com/library/windows/hardware/ff549303)元素，它确定设备是否由设备元数据包时操作系统使用的以下规则：

-   如果设备有一个模型 ID，操作系统不会搜索中的匹配项**HardwareIDList**元素。

-   否则，操作系统将搜索**HardwareIDList**设备硬件 ID 的匹配项的元素。

如果你的设备元数据包支持多个设备模型或模型 Id，可以指定[ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)为每个设备模型的元素。

以下是一种[ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303)元素中有多个**ModelID**元素：

```cpp
<ModelIDList>
<ModelID>825AAB98-18EE-4FE2-9472-197D1D00FE31</ModelID>
<ModelID>23F64715-AC4A-4DC4-B554-C8D56E43FE8B</ModelID>
</ModelIDList>
```

有关格式的要求的详细信息**ModelID** XML 元素，请参阅[ **ModelID**](https://msdn.microsoft.com/library/windows/hardware/ff549295)。

 

 





