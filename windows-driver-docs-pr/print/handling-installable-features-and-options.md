---
title: 处理可安装的功能和选项
description: 处理可安装的功能和选项
ms.assetid: b970808f-55bd-4a3a-9464-c9cd3567fa6f
keywords:
- Unidrv，可安装的功能和选项
- 可安装功能和选项 WDK Unidrv
- GPD 文件 WDK Unidrv，可安装功能和选项
- Unidrv WDK 打印
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: d9bc895385a652bc7f3f5f1c036b084eef0bb326
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638439"
---
# <a name="handling-installable-features-and-options"></a>处理可安装的功能和选项

打印机的某些功能或选项可能是可安装的。 例如，打印机可能会接受可选的信封进纸器，这可能是当前无法连接的。 必须通过两种方式在 GPD 文件中描述此信封进纸器：

- 作为 InputBin 功能的一个选项。

- 作为可安装的 "功能" （即使它确实是选项），这使用户能够指示它是否已实际安装。

首先，若要将信封进纸器与自动送纸器一起指定为 InputBin 功能的选项，可以使用以下 GPD 条目。

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

若要使信封送纸器可安装，需要额外的 GPD 条目，如下所示：

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

\*信封进纸器的选项条目中添加了两个属性：

- " \* 可安装的？" 属性表示选项是可安装的。

- \*InstallableFeatureName 属性指定 Unidrv 显示的文本字符串，以使用户能够指示该选项是否已实际安装。

每当功能或选项的** \* "可安装"** 设置为**TRUE**时，Unidrv 会为属性表显示创建附加功能。 （请注意，即使可安装项目是一个选项，Unidrv 也会在属性表中为其创建一个特征表示形式。）此 Unidrv 合成功能由** \* InstallableFeatureName**提供的字符串标识。 此功能提供了两个选项： "已安装" 和 "未安装"，并允许用户选择其中一个选项。 将 "已安装" 和 "未安装" 的字符串指定为 \* InstalledOptionName 和 \* NotInstalledOptionName 属性，以便您可以修改它们（如果其他文本更合适）。

因此，在我们的示例中，属性表包括一个标记为 " **Input Bin**" 的 InputBin 功能，其中包含两个选项，分别标记为**自动送纸器**和**信封进纸器**。 属性表还将包含一项附加功能，该功能**标记为****可选信封进** **Not installed** 如果首次选择 "在**可选信封进纸器****下"，** 则用户只能在 "**输入纸盒**" 下选择**信封进纸器**。

有时，有必要指出无法同时安装某些可安装选项，或者如果安装了其他某个可安装选项，则无法选择特定的 noninstallable 选项。 若要处理这些情况，请使用指定[选项约束](option-constraints.md)的 GPD 项。

不能将 "可 \* 安装？" 特性与需要 DisabledFeatures 项的可选功能一起使用 \* 。 对于这些功能，你必须显式指定带有 "已安装" 和 "未安装" 选项的可选功能。 例如，假设打印机有一个可选的双面打印单元。 如果未安装双面打印单元，则必须禁用双工功能（请参阅[标准功能](standard-features.md)）。 必须使用 "已安装" 和 "未安装" 选项来定义 "可选的双工单元" 功能。 在 "未安装" \* 选项条目中，你将 \* 为双工功能包含 DisabledFeatures 条目。 可以使用以下 GPD 条目：

```console
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

还应确保指定任何相关的[选项约束](option-constraints.md)，如图所示。
