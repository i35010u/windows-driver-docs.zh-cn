---
title: 处理可安装的功能和选项
description: 处理可安装的功能和选项
ms.assetid: b970808f-55bd-4a3a-9464-c9cd3567fa6f
keywords:
- Unidrv，可安装的功能和选项
- 可安装的功能和选项 WDK Unidrv
- GPD 文件 WDK Unidrv，可安装的功能和选项
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e470708dcfba3f2b5ef7256eecf36f574faa170
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564049"
---
# <a name="handling-installable-features-and-options"></a>处理可安装的功能和选项





某些打印机的功能或选项可能是可安装。 例如，打印机可以接受可选信封进纸器，这可能会或可能不当前连接。 此信封进纸器必须在两种方式 GPD 文件中所述：

-   作为一个选项来 InputBin 功能。

-   作为一个可安装的"功能"（即使它实际上是一个选项），它允许用户在以指示是否实际安装。

首先，要指定信封进纸器，以及一个自动送纸器，为 InputBin 功能选项，可以使用以下 GPD 条目。

```cpp
*Feature: InputBin
{
    *Name: "Input Bin"
    *Option: AUTO
    {
        *Name: "Automatic Feeder"
        *Command: CmdSelect {Command Attributes}
    }
    *Option: ENVFEED
    {
        *Name: "Envelope Feeder"
        *Command: CmdSelect {Command Attributes}
    }
}
```

若要使可安装信封进纸器，其他 GPD 条目所需，按如下所示：

```cpp
*InstalledOptionName: "Installed"
*NotInstalledOptionName: "Not installed"
*Feature: InputBin
{
    *Name: "Input Bin"
    *Option: AUTO
    {
        *Name: "Automatic Feeder"
        *Command: CmdSelect {Command Attributes}
    }
    *Option: ENVFEED
    {
        *Name: "Envelope Feeder"
        *Command: CmdSelect {Command Attributes}
        *Installable?: TRUE
        *InstallableFeatureName: "Optional Envelope Feeder"
    }
}
```

在\*选项条目已添加信封进纸器，两个属性：

-   \*可安装？ 属性指示是否可安装选项。

-   \*InstallableFeatureName 属性指定 Unidrv 显示，以便用户可以指示是否实际安装选项的文本字符串。

每当**\*可安装？** 设置为**TRUE** Unidrv 功能或选项，创建另一项功能以显示属性表。 （请注意，即使可安装的项是一个选项，Unidrv 功能表示为其创建属性表中。）此 Unidrv 合成功能由使用提供的字符串 **\*InstallableFeatureName**。 该功能提供了两个选项:"已安装"和"未安装"，并允许用户选择以下选项之一。 使用指定字符串"安装"和"未安装" \*InstalledOptionName 和\*NotInstalledOptionName 属性，以便更适合其他文本是否可以修改它们。

因此，对于本示例中，属性表包括 InputBin 功能，标记为**输入 Bin**，其中包括两个选项，标记为**自动送纸器**和**信封进纸器**. 属性表还应包括附加功能，标有**可选信封进纸器**，使用两个选项，标记为**已安装**并**未安装**。 用户只能选择**信封进纸器**下**输入 Bin**如果他或她首先选择**已安装**下**可选信封进纸器**.

有时，很有必要，以指示不能同时，安装某些可安装选项，或如果安装了其他一些可安装选项不能选择某个 noninstallable 选项。 若要处理这些情况下，使用指定的 GPD 条目[选项约束](option-constraints.md)。

不能使用\*可安装？ 属性的可选功能，需要使用\*DisabledFeatures 条目。 有关这些功能，必须显式指定可选的功能，使用"安装"和"未安装"选项。 例如，假设打印机具有可选双面打印单元。 双工功能 (请参阅[标准功能](standard-features.md)) 如果未安装进行双面打印单元，则必须禁用。 必须定义了"可选双面打印单元"功能，使用"已安装"和"未安装"选项。 在"未安装"\*选项条目应包括\*DisabledFeatures 条目的双工的功能。 可以使用以下 GPD 条目：

```cpp
*Feature: DuplexUnit
{
    *ConflictPriority: 3   *% Make priority higher than Duplex feature
    *Name: "Optional Duplexing Unit"
    *Option: Installed
    {
        *Name: "Installed"
    }
    *Option: NotInstalled
    {
        *Name: "Not Installed"
        *DisabledFeatures: LIST(Duplex)
        *Constraints: LIST (Duplex.LongEdge, Duplex.ShortEdge)
    }
}
```

请确保还指定任何相关[选项约束](option-constraints.md)，如下所示。

 

 




