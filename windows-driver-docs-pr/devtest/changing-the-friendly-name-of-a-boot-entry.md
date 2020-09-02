---
title: 更改启动项的友好名称
description: 更改启动项的友好名称
ms.assetid: 28f4f449-9027-453e-877a-d656539296c0
keywords:
- 命名 WDK 启动选项
- 友好名称 WDK 启动选项
- 重命名启动条目 WDK
- Boot.ini 文件 WDK，友好名称
- 启动选项 WDK，友好名称
ms.date: 01/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 015a3361b520456d5551a8d4d4b6e867fd05558a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383197"
---
# <a name="changing-the-friendly-name-of-a-boot-entry"></a>更改启动项的友好名称


在 Windows 中，在 Windows 启动管理器中显示的项是每个启动项的说明。

通常，在复制启动项后，您可以更改新创建项的友好名称，以便将其与原始项区分开来。

你还可以更改友好名称，以便更轻松地识别自定义的启动条目。 准确描述该条目的字符串可节省大量时间和精力。

例如，下面的友好名称字符串增加了小数值。

```
"Windows 10 Debug1"
"Windows 10 Debug2"
```

但是，更精确的字符串（如接下来的字符串）使启动选择更容易。

```
"Windows 10 kdnet"
"Windows 10 NullModem"
```

**注意**   如果将启动条目配置为调试 ([/debug/debugport](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)) 或紧急管理服务 (EMS) 在基于 x86 或 x64 的系统上 ([/redirect](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)) ，则启动加载程序 \[ 会在启动菜单中追加 (启用调试器 \] 或 \[ 启用 EMS) \] 的括号短语。
但是，如果友好名称和带括号的短语一起超过70个字符，则启动加载程序会在启动菜单中省略括号中的短语。 若要还原括起来的短语，请缩短友好名称。

若要更改 Boot.ini 文件中的启动项的友好名称，可以使用 Bootcfg 或在记事本中编辑 Boot.ini 文件。 在 EFI NVRAM 中存储启动选项的系统上，请使用 Bootcfg。

若要更改 Windows 的启动项的友好名称，请使用 BCDEdit。 

> [!CAUTION]
> 更新启动配置需要管理权限。 更改某些启动项选项可能会导致您的计算机无法操作。 


## <a name="span-idusing_bcdeditspanspan-idusing_bcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

若要更改启动菜单上显示的启动条目说明，可以使用 **/Set** *IDdescription* 选项。 该命令使用以下语法。 ID 是与启动项关联的 GUID (或众所周知的标识符之一，例如 {current} ) 。

> [!NOTE]
> 如果使用 [Windows PowerShell](/powershell/module/Microsoft.PowerShell.Core/?view=powershell-6)，必须使用引号将启动项标识符引起来，例如：“{49916baf-0e08-11db-9af4-000bdbd316a0}”或“{current}” 。


```console
bcdedit /set ID description "The new description"
```

例如：

```console
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} description "Windows 10 NullModem"
```

若要更改与当前运行的操作系统相对应的启动项的说明，请使用以下示例：

```console
bcdedit /set {current} description "Windows 10 NullModem"
```

你还可以在使用 **/d** 选项复制现有启动项时更改说明。

```console
bcdedit /copy {current} /d "Windows 10 NullModem"
```



## <a name="span-idusing_bootcfgspanspan-idusing_bootcfgspanusing-bootcfg"></a><span id="using_bootcfg"></span><span id="USING_BOOTCFG"></span>使用 Bootcfg

使用 Bootcfg，只能在复制项时更改启动项的友好名称。 使用 Bootcfg **/copy** 开关复制该条目，并更改其友好名称。

以下 Bootcfg 命令复制第一个启动条目以创建新条目。 **/Id**开关指定要复制的项的行号。 **/D** (说明) 开关指定新创建项的友好名称。

```console
bootcfg /copy /ID 1 /d "Windows 10 Debug"
```

有关使用 Bootcfg 的完整说明，请参阅 "帮助和支持服务"。 有关示例，请参阅 [使用启动参数](using-boot-parameters.md)。

## <a name="span-idediting_the_boot_ini_filespanspan-idediting_the_boot_ini_filespanediting-the-bootini-file"></a><span id="editing_the_boot_ini_file"></span><span id="EDITING_THE_BOOT_INI_FILE"></span>编辑 Boot.ini 文件

在 Boot.ini 文件中，启动项的友好名称显示在引导项的引号内。

例如，Boot.ini 文件中的以下示例具有适用于 Microsoft Windows 10 专业版的重复启动项。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```

若要更改启动项的友好名称，请在启动项中键入引用的字符串。 在下面的示例中，由于将自定义第一个项用于调试，因此，该名称将更改为 "Windows 10 调试"。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Windows 10 Debug" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```