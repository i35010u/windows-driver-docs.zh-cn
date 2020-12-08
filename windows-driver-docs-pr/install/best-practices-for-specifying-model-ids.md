---
title: 指定模型 ID 的最佳做法
description: 指定模型 ID 的最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63ee9a24f6e2888ebb47e4e2e2cd47bdf6a32573
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783185"
---
# <a name="best-practices-for-specifying-model-ids"></a>指定模型 ID 的最佳做法


模型 Id 基于业务定义或 (SKU) 的物理设备。 每个模型 ID 对于物理设备的所有构成和型号都必须是唯一的。

以下列表描述了物理设备的硬件 Id 和型号 Id 之间的差异：

-   [硬件 id](hardware-ids.md)是使用 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85)) xml 元素中的一个或多个 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) xml 元素指定的。 每个 **HardwareID** 值指定基于特定于总线的值的硬件函数。 硬件 Id 可用来将设备驱动程序映射到设备实例。

    例如，两个具有相同硬件 ID 的设备共享同一驱动程序使用的功能接口。

-   模型 Id 是使用 [**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) xml 元素中的一个或多个 [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) xml 元素指定的。 模型 Id 允许原始设备制造商 (OEM) 或独立硬件供应商 (IHV) ，以唯一标识与总线或接口技术无关的物理设备。

    例如，两个具有不同模型 Id 的设备可能为其组件具有相同的硬件 Id。

-   [硬件 id](hardware-ids.md) 用于将设备元数据包映射到特定总线或接口上的设备实例。

-   模型 Id 用于将设备元数据包映射到物理设备，无论设备连接到计算机的方式如何。

仅当 [**PackageInfo**](/previous-versions/windows/hardware/metadata/ff549574(v=vs.85)) xml 数据中未指定 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素时，才需要 [**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) xml 元素。 如果已指定，则 **ModelIDList** 元素必须包含一个或多个 [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) 元素，以便为设备支持的每个函数指定唯一的模型 ID。

如果 [**PackageInfo**](/previous-versions/windows/hardware/metadata/ff549574(v=vs.85)) XML 数据包含 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85)) 和 [**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) 元素，则当操作系统确定设备元数据包是否指定了设备时，操作系统将使用以下规则：

-   如果设备具有模型 ID，操作系统将不会在 **HardwareIDList** 元素中搜索匹配项。

-   否则，操作系统会在 **HardwareIDList** 元素中搜索设备的硬件 ID 的匹配项。

如果设备元数据包支持多个设备模型或模型 Id，则可以为每个设备模型指定一个 [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) 元素。

下面是包含多个 **ModelID** 元素的 [**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85))元素的示例：

```cpp
<ModelIDList>
<ModelID>825AAB98-18EE-4FE2-9472-197D1D00FE31</ModelID>
<ModelID>23F64715-AC4A-4DC4-B554-C8D56E43FE8B</ModelID>
</ModelIDList>
```

有关 **ModelID** XML 元素的格式要求的详细信息，请参阅 [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))。

 

