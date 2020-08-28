---
title: 添加启动项
description: 在 Windows Vista 和更高版本、Windows Server 2008 及更高版本以及 Windows 恢复环境中添加启动项
ms.assetid: 5027d7ea-6f8b-435a-849f-06727068d18b
keywords:
- 启动选项 WDK，添加启动条目
- 启动条目 WDK
- 添加启动条目
- Boot.ini 文件 WDK，添加启动条目
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42d09943529fd26e994021914b4d53958b64526
ms.sourcegitcommit: 9e5a99dc75dfee3caa9a242adc0ed22ae4df9f29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89043121"
---
# <a name="adding-boot-entries"></a>添加启动项


在操作系统中自定义启动选项的第一步是为操作系统添加新的 *启动条目* 。 *启动项*是一组用于定义操作系统或可启动程序的加载配置的选项。

对于一个操作系统，可以有多个启动条目，每个条目都有一组不同的启动参数。 Windows Installer 在安装操作系统时创建标准启动条目，你可以通过编辑启动选项为操作系统创建其他自定义的启动条目。

可以在 Windows Installer 创建的启动项中添加、删除和更改选项。 但是，保留标准条目是明智的，而应添加自定义的单独条目。

若要添加启动项，请复制现有启动项，然后修改副本。

本主题适用于 Windows Vista 和更高版本、Windows Server 2008 及更高版本以及 Windows 恢复环境。

## <a name="adding-a-new-boot-entry"></a>添加新的启动条目 <a name="adding-a-new-boot-entry-in-windows-vista-and-later"></a>

在 Windows 中，可以使用 BCDEdit 来修改启动选项。 若要添加新的启动条目，请使用提升的权限打开命令提示符窗口 (选择并按住 (或右键单击) **命令提示符** ，然后从快捷菜单) 中选择 "以 **管理员身份运行** "。

**注意**   设置 BCDEdit 选项之前，你可能需要在计算机上禁用或暂停 BitLocker 和安全启动。

 

创建新启动条目的最简单方法是复制现有条目，然后根据需要进行修改。 为此，请结合使用 BCDEdit 和 **/copy** 选项。 例如，在下面的命令中，BCDEdit 将上次用于启动 Windows 的 Microsoft Windows 启动条目（标识为 **{current}**）复制，并创建新的启动条目。 **/D** description 选项将 DebugEntry 指定为新启动条目的名称。

```
bcdedit /copy {current} /d "DebugEntry"
```

如果命令成功，则 BCDEdit 会显示类似于以下内容的消息：

```
The entry was successfully copied to {49916baf-0e08-11db-9af4-000bdbd316a0}.
```

当你复制出现在启动菜单上的启动加载程序项时，该副本将自动添加为启动菜单上的最后一项。

上述消息中的 GUID (出现在大括号 ({}) # A3 之间，是新启动条目的标识符。 **/Copy**选项为启动条目创建新的 GUID。 使用标识符表示所有后续 BCDEdit 命令中的条目。

如果命令失败，请确保在具有管理员权限的命令提示符窗口中运行，并且所有命令参数拼写正确，包括围绕 **{current}** 的大括号。

还可以使用 **/create** 选项添加启动项。 此方法更难，因为需要提供有关启动项类型的其他信息。 还需要指定 **/application**、 **/inherit**或 **/device** 选项。 例如，以下示例创建名为 "我的 Windows Vista" 的新操作系统启动项：

```
bcdedit /create /d "My Windows Vista" /application osloader
```

使用 **/create** 选项时，不会自动将新的启动加载程序条目添加到启动菜单。 **/Create**选项为启动项创建新的 GUID。 必须使用 **/displayorder** 选项将新的启动条目添加到启动菜单。 可以按任意顺序放置启动加载程序条目。

有关 **/create** 命令参数的信息，请在命令提示符窗口中键入 **bcdedit/？/create** 。

## <a name="editing-the-boot-menu"></a>编辑启动菜单 <a name="editing-the-boot-menu-in-windows-vista-and-later"></a>

在 Windows 中，不会自动将新的启动加载程序条目添加到启动菜单。 可以按任意顺序放置启动加载程序条目。

可以使用 **/displayorder** 选项来设置启动管理器在多启动菜单上显示启动条目的顺序。 该命令具有以下语法：

```
bcdedit /displayorder {ID} {ID} ...
```

ID 是启动项的 GUID 或保留标识符，如 **{current}**) 。 用空格分隔每个标识符。 请确保) 中包含大括号 ({} 。

例如，若要将 DebugEntry boot 条目添加到 "启动" 菜单中的 **{current}** 项后，请使用以下命令 (记得 `'{guid}'` 在 Windows PowerShell 中使用) ：

```
bcdedit /displayorder {current} {49916baf-0e08-11db-9af4-000bdbd316a0}
```

还可以使用选项 **/addlast、/addfirst**和 **/remove** 从菜单中订购和删除项目。 例如，以下命令将 DebugEntry boot 条目作为菜单上的最后一项添加：

```
bcdedit /displayorder {49916baf-0e08-11db-9af4-000bdbd316a0} /addlast
```

## <a name="removing-and-deleting-a-boot-entry"></a>删除和删除启动项 <a name="removing-a-boot-entry-in-windows-vista-and-later"></a>

以下命令将从启动菜单中删除 {49916baf-0e08-11db-9af4-000bdbd316a0} 启动条目项。

```
bcdedit /displayorder {49916baf-0e08-11db-9af4-000bdbd316a0} /remove
```

使用 **/displayorder** 和 **/remove** 选项删除指定的启动项目时，启动项目将从启动菜单中删除，但它仍在 BCD 存储中。 若要从启动菜单和应用商店中完全删除启动加载器项，请使用 **/delete** 选项。

```
bcdedit /delete {49916baf-0e08-11db-9af4-000bdbd316a0}
```

若要验证显示顺序是否正确，请使用以下命令：

```
bcdedit
```

如果键入 **bcdedit** 时没有其他参数，则 bcdedit 会按照它们在菜单中出现的顺序显示启动管理器项和启动加载程序项。

Windows 启动管理器项还包括启动菜单显示顺序，如下面的示例所示。

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
