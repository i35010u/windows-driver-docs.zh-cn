---
title: 设备筛选器驱动程序排序
description: Microsoft 开发了一种以声明方式添加筛选器的方法，，此方法称为“设备筛选器驱动程序排序”，表达的是筛选器的意图而不是堆栈位置。
ms.date: 04/16/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c146762cf55ceb51c081c0852fa966424e6df221
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "69887200"
---
# <a name="device-filter-driver-ordering"></a>设备筛选器驱动程序排序

Microsoft 开发了一种以声明方式添加筛选器的方法，，此方法称为“设备筛选器驱动程序排序”，表达的是筛选器的意图而不是堆栈位置。

## <a name="the-need-for-device-filter-driver-ordering"></a>对设备筛选器驱动程序排序的需求

在 Windows 10 版本 1903 之前，注册设备筛选器驱动程序的唯一受支持方法是添加注册表项（使用 [AddReg 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)）。 但是，这种注册表操作方法不能灵活指定要将特定筛选器注册到的**确切位置**。

使用 AddReg 指令的筛选器注册只会将筛选器追加到筛选器列表的末尾。 此方法使用值的列表，其中的顺序非常重要，决定了要将筛选器加载到堆栈中的哪个位置。

使用单个有序值列表这一方法不太理想，尤其是当 [AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) 只追加到末尾时，因为在有多个驱动程序将筛选器添加到同一设备时，会造成不利后果。   

在至少涉及到一个[扩展 INF](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file) 的情况下，如果 INF 不当使用 **AddReg**（即，不使用追加标志），则它们可能会擦除掉另一 INF 添加的筛选器。

此外，多个扩展 INF 可能会添加筛选器，而这些筛选器的相对顺序可能很重要；但是，即插即用 (PnP) 平台不保证扩展的安装顺序。 结果是不能保证“追加”顺序。

## <a name="implementing-device-filter-driver-ordering"></a>实现设备筛选器驱动程序排序

为了提供灵活的声明方法来注册设备筛选器，Microsoft 开发了一种以声明方式添加筛选器的方法，，此方法表达的是筛选器的意图而不是堆栈位置。 该解决方案可让函数驱动程序作者在其 INF 中表达筛选器可将自身注册到的**有序位置集（称为级别）** 。

除了特定的级别以外，筛选器还能以声明方式简单注册为高级别或低级别筛选器。  

基础结构基于新的筛选器注册方法，可确定要在设备堆栈中包含哪些顺序驱动程序。 新方法不会破坏与添加筛选器的旧方法的兼容性。 但是，它确实可以让新的筛选器过渡到更可靠、更灵活的注册机制。

让基础 INF 定义一个或多个“级别”的有序列表即可启用该方法。 基础 INF 和任何扩展 INF 可以通过一个新的 INF 指令注册声明筛选器，该指令指定该筛选器所属的服务名称和级别。 每个高级别和低级别筛选器由其相应的级别有序列表表示。

这些高级别和低级别筛选器列表是通过按级别排序所有筛选器驱动程序创建的。 应将每个级别中的筛选器顺序视为“任意”，特定级别中的筛选器顺序不能存在依赖关系。  如果必须**保证**两个筛选器的相对顺序，应将其注册到不同的级别。

考虑以下设备驱动程序示例：

![设备驱动程序的安装以设备堆栈顺序显示，其中合并了筛选器驱动程序列表，同时遵循所需的位置和排序。](images/device_filter_ordering_1.png)

设备驱动程序的基础 INF 声明两个较高的筛选器级别：A 和 B（遵循此顺序）。 在基础 INF 的关联扩展 INF 中，已将两个筛选器添加到这两个级别中的每一个。

设备驱动程序安装的结果是一个设备堆栈顺序，其中合并了筛选器驱动程序列表，同时遵循所需的位置和排序。 最终的设备堆栈顺序确保“A”级别中放置的任何筛选器位于“B”级别中任何筛选器的前面。 但是，在每个级别中，顺序是任意的。

如示例中所示，Filter3 可能位于 Filter5 的前面，也可能位于 Filter5 的后面。 在任何情况下，Filter3 和 Filter5 都位于下一级别“B”中筛选器的前面。

在设计筛选器可注册到的级别系列时，请不要出于排序目的创建级别系列，而应该按照将级别映射到筛选器意图的方式命名和排序级别。 例如，I/O 设备可以定义任何加密筛选器应注册到的“加密”级别。  这样就可以轻松理解和管理筛选器的意图，并使堆栈变得更可靠，可以应对函数驱动程序发生的重大更改。

> [!NOTE]
> 即使不使用基础 INF 定义的级别，声明筛选器也可以方便地注册为高级别或低级别筛选器。 未定义级别时，此过程在逻辑上相当于将筛选器追加到 UpperFilters/LowerFilters 注册表值的末尾。 定义了级别时，必须将某个级别标记为基础驱动程序中的默认级别，在这种情况下，筛选器将注册到该级别。

## <a name="scenarios"></a>方案

考虑一个对通过堆栈的数据进行加密的 I/O 设备驱动程序。 为此，典型的实现可能会紧接在函数驱动程序的下方使用一个低级别的筛选器驱动程序。 为了确保加密筛选器放在驱动程序作者所需的确切位置，他们可以按如下所示使用声明筛选器：

![图中显示，通过将“加密”筛选器驱动程序明确放在“加密”级别中，该驱动程序可确保最终的设备堆栈顺序会将“加密”筛选器驱动程序放在其他更低级别的所有筛选器的前面，并紧接在函数驱动程序的后面。](images/device_filter_ordering_2.png)

基础 INF 将建立筛选器的两个低级别：“\"加密\"”和“监视”（默认设置）。 此示例中的“监视”（默认设置）是此特定设备可能存在的其他低级别筛选器。 通过将“加密”筛选器驱动程序明确放在“加密”级别中，该驱动程序可确保最终的设备堆栈顺序会将“加密”筛选器驱动程序放在其他更低级别的所有筛选器的前面，并紧接在函数驱动程序的后面。

让我们进一步分析该示例。 假设该驱动程序推出了更新的版本，并且作者在函数驱动程序中内置了加密。 这样就不需要单独的“加密”筛选器驱动程序。 作者只需从基础 INF 中删除包含“加密”筛选器的级别，当驱动程序更新时，堆栈会再次动态生成。

如果某个筛选器将自身声明为位于一个不存在的级别中，该筛选器最终不会进入设备堆栈。 在该示例中，基础 INF 已更新，即使扩展 INF 保持不变，但最终的设备堆栈会排除“加密”筛选器，因为该筛选器不包含在基础 INF 的级别声明中。

![演示从基础 INF 中删除包含“加密”筛选器的级别的示意图](images/device_filter_ordering_3.png)

## <a name="default-filter-level"></a>默认筛选器级别

为了生成最终的筛选器堆栈，所有筛选器信息源将合并到单个列表。 必须注意，合并逻辑是**在创建设备堆栈时**执行的。 如果通过安装新的/更新的基库或扩展驱动程序添加了新的筛选器，则设备将在安装过程中重启，并选取新的筛选器列表。

某些筛选器源缺少所有位置信息，这些筛选器是通过传统的 UpperFilters/LowerFilters 注册表值或通过仅限位置的声明语法（下面将会介绍）添加的。

若要在缺少位置信息时支持有效合并，基础 INF 必须定义附加的信息片段：默认筛选器级别。 默认筛选器级别是缺少级别或位置信息的筛选器要插入到的位置。

例如，可在基础 INF 中定义如下所示的筛选器级别：

```INF
Level Order: A, B, C
DefaultFilterLevel: C
```

将默认级别指定为最终级别表示缺少位置信息的任何筛选器将**追加**到筛选器列表。 或者，驱动程序作者可能希望最终的堆栈中始终包含已显式注册到 C 的筛选器：

```INF
Level Order: A, B, C
DefaultFilterLevel: B
```

由于默认筛选器级别设置为 B，不包含位置信息的任何附加筛选器将插入到 A 级别筛选器和 C 级别筛选器之间。

## <a name="syntax"></a>语法

### <a name="registering-filters"></a>注册筛选器

```INF
[DDInstall.Filters]
AddFilter = <FilterName>, [Flags], FilterSection
```

可按以下两种方式之一指定 FilterLevel 或 FilterPosition：

**选项 1：**

```INF
[FilterSection]
FilterLevel=<LevelName>
```

**选项 2：**

```INF
FilterPosition=Upper/Lower
```

可以在基础 INF **和**扩展 INF 中完成此操作。

\[DDInstall.Filters\]

**FilterName** 是服务在系统中的名称。

**Flags** 当前未使用，应保留为空或设置为 0。

**FilterSection** 是描述筛选器的节。

\[筛选器节\]

筛选器节只能包含以下两个指令中的一个：  **FilterLevel** 或 **FilterPosition**。

**FilterLevel** 是堆栈上的要将设备筛选器插入到的特定位置，由基础 INF 定义。  在每个级别中，筛选器的顺序是任意的。

如果类中包含一个要将第三方筛选器插入到的位置，则会使用 **FilterPosition**。

### <a name="defining-filter-levels"></a>定义筛选器级别

```INF
[DDInstall.HW]
AddReg = FilterLevel_Definition

[FilterLevel_Definition]
HKR,,UpperFilterLevels,%REG_MULTI_SZ%,"LevelA","LevelB","LevelC"
HKR,,UpperFilterDefaultLevel,,"LevelC"

HKR,,LowerFilterLevels,%REG_MULTI_SZ%,"LevelD","LevelE","LevelF"
HKR,,LowerFilterDefaultLevel,,"LevelE"
```

只能通过**基础**驱动程序完成此操作。

查询以下属性可以检索特定设备的完整筛选器声明列表：

```INF
DEVPKEY_Device_CompoundUpperFilters
DEVPKEY_Device_CompoundLowerFilters
```

### <a name="legacy-equivalent-filter-registration"></a>传统的等效筛选器注册

让我们探讨如何使用传统方法通过 INF 尝试添加一个高级别的筛选器：

```INF
[DDInstall.HW]
AddReg = Filters

[Filters]
HKR,,"UpperFilters", 0x00010008, "MyFilter"
```

此语法将“MyFilter”添加到高级别筛选器列表的末尾。

使用引入的新语法，以上代码节在逻辑上类似于：

```INF
[DDInstall.Filters]
AddFilter = MyFilter,,MyUpperFilterInstall

[MyUpperFilterInstall]
FilterPosition = Upper
```

此代码指定要将筛选器“MyFilter”添加到高级别筛选器列表。 如果基础 INF 已指定筛选器级别，则使用 *FilterPosition* 会在该位置的默认级别中注册筛选器。

如果未指定筛选器级别，此筛选器将注册为采用任意顺序的高级别筛选器。
