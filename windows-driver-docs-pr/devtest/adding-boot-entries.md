---
title: 添加启动项
description: 添加启动项在 Windows Vista 及更高版本、 Windows Server 2008 和更高版本、 和 Windows 恢复环境
ms.assetid: 5027d7ea-6f8b-435a-849f-06727068d18b
keywords:
- 启动选项 WDK，添加启动项
- 启动项 WDK
- 添加启动项
- Boot.ini 文件 WDK，添加启动项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 674a3afeb59ff74b5830d2350267d435fc507da3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569207"
---
# <a name="adding-boot-entries"></a>添加启动项


自定义启动选项在操作系统中的第一步是添加一个新*引导条目*操作系统。 一个*引导条目*是一组定义的操作系统或可启动的程序的负载配置的选项。

可以具有多个操作系统，每个都有一组不同的启动参数启动项。 安装操作系统，并可以通过编辑启动选项来创建操作系统的附加的自定义启动项时，Windows 安装程序创建的标准启动项。

您可以添加、 删除和更改 Windows 安装程序创建的启动项目中的选项。 但是，它是比较明智的做法是，若要保留的标准条目和，相反，请添加自定义的单独条目。

若要添加的启动项，复制现有的启动项目，并修改该副本。

本主题适用于 Windows Vista 和更高版本，Windows Server 2008 及更高版本，以及 Windows 恢复环境。

## 添加新的启动项目 <a name="adding-a-new-boot-entry-in-windows-vista-and-later"></a>

在 Windows 中，使用 BCDEdit 修改您的启动选项。 若要添加的新的启动项，请使用提升的权限打开命令提示符窗口 (右键单击**命令提示符**然后单击**以管理员身份运行**从快捷菜单)。

**请注意**  之前设置可能需要禁用或暂停 BitLocker 和安全启动的计算机上的 BCDEdit 选项。

 

若要创建的新的启动项的最简单方法是复制现有条目，然后根据需要修改它。 若要执行此操作，请使用与 BCDEdit **/复制**选项。 例如，在以下命令，BCDEdit 将上次使用的 Microsoft Windows 启动项目到启动 Windows，标识为 **{当前}**，并创建新的启动项目。 **/D**说明选项指定 DebugEntry 作为新的启动项目的名称。

```
bcdedit /copy {current} /d "DebugEntry"
```

如果命令成功，BCDEdit 将显示一条类似于以下消息：

```
The entry was successfully copied to {49916baf-0e08-11db-9af4-000bdbd316a0}.
```

复制时显示在启动菜单的启动加载程序项，该副本是自动添加作为引导菜单中的最后一项。

前面的消息中的 GUID (大括号之间显示 ({})) 是新的启动项目的标识符。 **/复制**选项创建新的 GUID 的启动项目。 标识符用于表示所有后续的 BCDEdit 命令中的条目。

如果该命令将失败，请确保正在使用管理员权限的命令提示符窗口中运行，并且，所有命令参数拼写正确，包括两边的括号 **{当前}**。

您还可以添加启动项使用 **/ 创建**选项。 此方法是更加困难，因为你需要提供有关启动条目类型的其他信息。 此外需要指定 **/应用程序**， **/ 继承**，或 **/device**选项。 例如，下面的示例创建名为"我的 Windows Vista"的新操作系统启动项：

```
bcdedit /create /d "My Windows Vista" /application osloader
```

当你使用 **/ 创建**选项，新的引导加载程序条目不会自动添加到启动菜单。 **/ 创建**选项创建新的 GUID 的启动项目。 您必须使用新的引导条目添加到引导菜单 **/displayorder**选项。 您可以按任何顺序放置的启动加载程序项。

璝惠 **/ 创建**命令参数中，键入**bcdedit /？ / 创建**在命令提示符窗口中。

## 编辑启动菜单 <a name="editing-the-boot-menu-in-windows-vista-and-later"></a>

在 Windows 中，新的引导加载程序项将不自动添加到启动菜单。 您可以按任何顺序放置的启动加载程序项。

可以使用 **/displayorder**选项设置在其中启动管理器将多引导菜单显示的启动项的顺序。 该命令的语法如下：

```
bcdedit /displayorder {ID} {ID} ...
```

ID 是 GUID 的启动项目或保留的标识符，例如 **{当前}**)。 请用空格分隔每个标识符。 请务必包括大括号 ({})。

例如，若要对启动菜单后添加的 DebugEntry 启动项目 **{当前}** 条目，请使用以下命令 (请记住使用`'{guid}'`Windows PowerShell 中):

```
bcdedit /displayorder {current} {49916baf-0e08-11db-9af4-000bdbd316a0}
```

此外可以使用选项 **/addlast、 /addfirst**，并 **/remove**以进行排序和从菜单中删除项。 例如，以下命令将作为菜单上的最后一项添加的 DebugEntry 启动项目：

```
bcdedit /displayorder {49916baf-0e08-11db-9af4-000bdbd316a0} /addlast
```

## 删除和删除的启动项 <a name="removing-a-boot-entry-in-windows-vista-and-later"></a>

以下命令从启动菜单移除 {49916baf-0e08-11db-9af4-000bdbd316a0} 启动条目项。

```
bcdedit /displayorder {49916baf-0e08-11db-9af4-000bdbd316a0} /remove
```

删除指定的启动项使用时 **/displayorder**并 **/remove**选项，从启动菜单中，删除的启动项目，但它仍处于 BCD 存储。 若要完全删除引导加载程序项，从启动菜单中，从应用商店，请使用 **/delete**选项。

```
bcdedit /delete {49916baf-0e08-11db-9af4-000bdbd316a0}
```

若要验证的显示顺序正确，请使用以下命令：

```
bcdedit
```

当您键入**bcdedit**不使用其他参数，BCDEdit 显示启动管理器入口和启动加载程序条目将显示在菜单的顺序。

Windows 启动管理器条目还包括启动菜单显示顺序，如以下示例所示。

```
## Windows Boot Manager
identifier              {bootmgr}
device                  partition=C:
description             Windows Boot Manager
locale                  en-US
inherit                 {globalsettings}
default                 {current}
displayorder            {current}
                        {18b123cd-2bf6-11db-bfae-00e018e2b8db}
toolsdisplayorder       {memdiag}
timeout                 30

## Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             Microsoft Windows Vista
locale                  en-US
inherit                 {bootloadersettings}
osdevice                partition=C:
systemroot              \Windows
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn

## Windows Boot Loader
-------------------
identifier              {18b123cd-2bf6-11db-bfae-00e018e2b8db}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             Debugger Boot
locale                  en-US
inherit                 {bootloadersettings}
osdevice                partition=C:
systemroot              \Windows
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn
debug                   Yes
```
