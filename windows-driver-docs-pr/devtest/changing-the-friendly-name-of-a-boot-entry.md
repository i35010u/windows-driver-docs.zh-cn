---
title: 更改启动项的友好名称
description: 更改启动项的友好名称
ms.assetid: 28f4f449-9027-453e-877a-d656539296c0
keywords:
- 名称 WDK 启动选项
- 友好名称 WDK 启动选项
- 重命名的启动项 WDK
- Boot.ini 文件 WDK，友好名称
- 启动选项 WDK，友好名称
ms.date: 01/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: f5c5b21ba678ae6d82d6f9de835bd4b805412a14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343985"
---
# <a name="changing-the-friendly-name-of-a-boot-entry"></a>更改启动项的友好名称


在 Windows、 Windows 启动管理器中显示的项是每个启动项目的说明。

通常情况下，将复制的启动项后，您将更改新创建的项，以使其不同于原始的友好名称。

此外可以更改友好名称以使其更轻松地识别自定义的启动项。 准确地描述该条目的字符串可以节省大量的时间和精力。

例如，以下友好名称字符串添加没有意义。

```
"Windows 10 Debug1"
"Windows 10 Debug2"
```

但是，更精确的字符串，例如遵循，请启动所选容易得多。

```
"Windows 10 kdnet"
"Windows 10 NullModem"
```

**请注意**  的启动项配置为调试时 ([/debug /debugport](https://msdn.microsoft.com/library/windows/hardware/ff556253)) 或紧急管理服务 (EMS) ([/重定向](https://msdn.microsoft.com/library/windows/hardware/ff557180)) 上 x86-或基于 x64 的系统，启动加载程序将追加一个用括号括起来的短语 (\[启用调试器\]或\[ems 启用\]) 到在启动菜单中显示的友好名称。
但是，启动加载程序的友好名称和用括号括起来的短语一起超过 70 个字符时忽略从启动菜单带中括号的短语。 若要还原用括号括起来的短语，缩短的友好名称。

若要更改 Boot.ini 文件中的启动项的友好名称，可以使用 Bootcfg 或编辑在记事本中的 Boot.ini 文件。 在系统上存储在 EFI NVRAM 中的启动选项，使用 Bootcfg。

若要更改 Windows 的启动项的友好名称，请使用 BCDEdit。 

> [!CAUTION]
> 更新的启动配置所需管理权限。 更改某些启动项选项可能导致您的计算机无法运行。 


## <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

若要在启动菜单上出现更改启动项目的说明，可以使用 **/set** *IDdescription*选项。 该命令使用以下语法。 ID 是与启动项 （或一个已知的标识符，例如，{当前}） 相关联的 GUID。

> [!NOTE]
> 如果使用的[Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=108518)，必须使用引号将启动条目标识符，例如： **"{49916baf-0e08-11db-9af4-000bdbd316a0}"** 或 **"{current}"**.


```console
bcdedit /set ID description "The new description"
```

例如：

```console
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} description "Windows 10 NullModem"
```

若要更改对当前正在运行的操作系统相对应的启动项目的说明，请使用下面的示例：

```console
bcdedit /set {current} description "Windows 10 NullModem"
```

复制现有的启动项使用时，还可以更改描述 **/d**选项。

```console
bcdedit /copy {current} /d "Windows 10 NullModem"
```



## <a name="span-idusingbootcfgspanspan-idusingbootcfgspanusing-bootcfg"></a><span id="using_bootcfg"></span><span id="USING_BOOTCFG"></span>使用 Bootcfg

使用 Bootcfg，可以复制该条目时仅更改的启动项的友好名称。 使用 Bootcfg **/复制**开关来复制该条目，并更改其友好名称。

以下 Bootcfg 命令将复制的第一个启动项目以创建新条目。 **/ID**开关指定要复制的项的行号。 **/D** （说明） 开关指定的新创建的项的友好名称。

```console
bootcfg /copy /ID 1 /d "Windows 10 Debug"
```

有关使用 Bootcfg 的完整说明，请参阅帮助和支持服务。 有关示例，请参阅[使用引导参数](using-boot-parameters.md)。

## <a name="span-ideditingthebootinifilespanspan-ideditingthebootinifilespanediting-the-bootini-file"></a><span id="editing_the_boot_ini_file"></span><span id="EDITING_THE_BOOT_INI_FILE"></span>编辑 Boot.ini 文件

在 Boot.ini 文件中，在引号中的启动项目中将显示的启动项的友好名称。

例如，下面的示例从 Boot.ini 文件的重复启动项有 Microsoft Windows 10 专业版。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```

若要更改的启动项的友好名称，请键入覆盖的启动项目中的带引号的字符串。 在以下示例中，第一个条目将自定义以进行调试，因为名称更改为 Windows 10 调试。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Windows 10 Debug" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```
