---
title: 用于启用 EMS 重定向的启动参数
description: 用于启用 EMS 重定向的启动参数
ms.assetid: b93fd580-0e1d-4b1e-8358-1c6ce7e2eb5e
keywords:
- 引导参数 WDK
- 启动入口参数 WDK
- 紧急管理服务 WDK 引导参数
- EMS 重定向 WDK 引导参数
- 远程管理 WDK 引导参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c341bc214f659a3b4fc5c023c778c2af4993d17f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360415"
---
# <a name="boot-parameters-to-enable-ems-redirection"></a>用于启用 EMS 重定向的启动参数

紧急管理服务 (EMS) 技术允许您远程，控制服务器的所选的组件，即使服务器未连接到网络或其他标准的远程管理工具。 EMS 支持所有版本的 Windows Server 2003 操作系统 x86-、 x64-，和基于 Itanium 的计算机上。

> [!NOTE]
> 本主题说明如何在运行 Windows Server 2003 的计算机上启用 EMS。 在 Windows Vista 或更高版本的 Windows 上不支持在本部分中所述的启动参数。
> 启动加载程序的启动项配置时用于 EMS 使用 BIOS 固件的计算机上，将用括号括起来的短语，追加\[ems 启用\]，到在启动菜单显示的友好名称。 但是，启动加载程序的友好名称和用括号括起来的短语一起超过 70 个字符时忽略从启动菜单带中括号的短语。 若要还原用括号括起来的短语，缩短的友好名称。

若要确定计算机是否具有 ACPI 固件，使用设备管理器 (devmgmt.msc)。 在设备管理器中，展开**计算机**节点。 ACPI 固件，节点下的名称的计算机上**计算机**中包含单词**ACPI**。

## <a name="enabling-ems-on-a-computer-without-an-acpi-spcr-table-in-operating-systems-prior-to-windows-server-2008"></a>没有 Windows Server 2008 之前的操作系统中的 ACPI SPCR 表的计算机上启用 EMS

若要启用 EMS 控制台重定向的计算机具有 BIOS 固件，但不具有 ACPI 串行端口控制台重定向 (SPCR) 表上，添加 **重定向 = COM * * * x*并**redirectbaudrate =** 为参数\[启动加载器\]Boot.ini 文件部分。 这些参数设置为 EMS 控制台重定向的端口和传输速率。 在 BIOS 中的带外通信使用相同的端口和传输速率建立的。 然后，添加[ **/重定向**](https://docs.microsoft.com/windows-hardware/drivers/devtest/-redirect)的启动项的参数。

以下 Bootcfg 命令启用 EMS 控制台重定向对列表中的第一个启动项目。 它为 COM2 设置的端口，并设置的传输速率为 115,200 千位 / 秒 (Kbps)。 这些是相同的端口和波特率率设置了管理员在带外端口 BIOS 设置。

```command
bootcfg /ems ON /port COM2 /baud 115200 /id 1
```

以下 Bootcfg 屏幕将显示命令的结果。 新添加的参数以粗体显示。

```command
## Boot Loader Settings
timeout:          3
default:          multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
redirect:         COM2
redirectbaudrate: 115200

Boot Entries
------------
Boot entry ID:   1
Friendly Name:   "Windows Server 2003, Standard with EMS"
Path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
OS Load Options: /fastdetect /redirect
```

下面的示例演示上一个示例 Boot.ini 文件相同的命令的结果。

```command
[boot loader]
timeout=1
default=multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect=COM2
redirectbaudrate=115200
[operating systems]
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="EMS boot" /fastdetect /redirect
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="Windows Server 2003, Standard" /fastdetect
```

## <a name="enabling-ems-on-a-computer-without-an-acpi-spcr-table-in-windows-server-2008"></a>启用 Windows Server 2008 中的 ACPI SPCR 表没有的计算机上的 EMS

若要启用 EMS 控制台重定向的计算机具有 BIOS 固件，但不具有 ACPI 串行端口控制台重定向 (SPCR) 表上，使用[ **BCDEdit /emssettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--emssettings)命令以设置 COM 端口和波特率。

这些参数设置为 EMS 控制台重定向的全局端口和传输速率。 在 BIOS 中的带外通信使用相同的端口和传输速率建立的。

然后，使用[ **BCDEdit /ems** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--ems)命令为启动项目启用 EMS。

以下命令设置全局 EMS 重定向设置，以使用 COM2 和波特率为 115200，并为指定的启动项目启用 EMS。

```command
bcdedit /emssettings EMSPORT:2 EMSBAUDRATE:115200
```

```command
bcdedit /ems {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

## <a name="enabling-ems-on-a-computer-with-an-spcr-table-in-operating-systems-prior-to-windows-server-2008"></a>Windows Server 2008 之前的操作系统中的一个 SPCR 表使用的计算机上启用 EMS

若要使用 ACPI BIOS 固件和 ACPI SPCR 表的计算机上启用 EMS，你可以使用**重定向 = USEBIOSSETTINGS**参数或 **重定向 = COM * * * x*和**redirectbaudrate =** 参数。 然后，可以添加[ **/重定向**](https://docs.microsoft.com/windows-hardware/drivers/devtest/-redirect)的启动项的参数。

下面的示例说明如何使用**重定向 = USEBIOSSETTINGS**参数。 以下 Bootcfg 命令启用 EMS 控制台重定向对列表中的第一个启动项目。

```command
bootcfg /ems ON /port BIOSSET /id 1
```

以下 Bootcfg 屏幕将显示命令的结果。 新添加的参数以粗体显示。

```command
## Boot Loader Settings
timeout: 1
default: multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect:USEBIOSSETTINGS

Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: EMS boot
Path:             multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
OS Load Options:  /fastdetect /redirect

Boot entry ID:    2
OS Friendly Name: Windows Server 2003, Standard
Path:             multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
OS Load Options:  /fastdetect
```

下面的示例演示上一个示例 Boot.ini 文件相同的命令的结果。

```command
[boot loader]
timeout=1
default=multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect=USEBIOSSETTINGS
[operating systems]
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="EMS boot" /fastdetect /redirect
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="Windows Server 2003, Standard" /fastdetect
```

## <a name="enabling-ems-on-a-computer-with-an-spcr-table-in-windows-server-2008"></a>Windows Server 2008 中的 SPCR 表使用的计算机上启用 EMS

若要使用 ACPI BIOS 固件和 ACPI SPCR 表的计算机上启用 EMS，可以使用[ **BCDEdit /emssettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--emssettings)并指定**BIOS**参数或**emsport**并**emsbaudrate**参数。 若要为启动项目启用 EMS，请使用[ **BCDEdit /ems** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--ems)命令。

下面的示例演示如何使用**BIOS**参数。 以下的 BCDEdit 命令启用 EMS 控制台重定向对当前启动项目。

```command
bcdedit /emssettings bios
bcdedit /ems on
```

## <a name="enabling-ems-on-a-computer-with-efi-firmware-in-operating-systems-prior-to-windows-server-2008"></a>使用 Windows Server 2008 之前的操作系统中的 EFI 固件的计算机上启用 EMS

若要使用 EFI 固件的计算机上启用 EMS，请使用 Bootcfg 添加[ **/重定向**](https://docs.microsoft.com/windows-hardware/drivers/devtest/-redirect)的启动项的参数。 Windows 通过阅读 SPCR 表在固件中查找带的端口和其设置，并使用相同的端口和速率 EMS 控制台重定向。

以下 Bootcfg 命令启用 EMS 基于 Itanium 的计算机上的重定向。 它使用 Bootcfg **/ems**开关与要添加的 ON 参数 **/重定向**启动项的参数。 **/Id**开关标识的启动项目。

```command
bootcfg /ems ON /id 1
```

Bootcfg 显示在下面的 EFI NVRAM 中的启动选项显示 Bootcfg 命令的结果。 第一个启动项配置为启用 EMS 控制台重定向加载操作系统。

```command
Boot Options
------------
Timeout:             30
Default:             \Device\HarddiskVolume3\WINDOWS
CurrentBootEntryID:  1

Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise with EMS
OsLoadOptions:     /fastdetect /redirect
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS
```

## <a name="enabling-ems-on-a-computer-with-efi-firmware-in-windows-server-2008"></a>使用 Windows Server 2008 中的 EFI 固件的计算机上启用 EMS

若要使用 EFI 固件的计算机上启用 EMS，请使用[ **BCDEdit /ems** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--ems)命令并指定的启动项。 Windows 通过阅读 SPCR 表在固件中查找带的端口和其设置，并使用相同的端口和速率 EMS 控制台重定向。

以下命令启用 EMS 控制台重定向对具有 {18b123cd-2bf6-11db-bfae-00e018e2b8db} 的标识符指定的启动项。

```command
bcdedit /ems {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

## <a name="changing-ems-settings-on-a-computer-with-bios-firmware-in-operating-systems-prior-to-windows-server-2008"></a>使用 Windows Server 2008 之前的操作系统中的 BIOS 固件的计算机上的更改 EMS 设置

在 EMS 配置上的一个启动项时，添加**重定向 =** 参数\[启动加载器\]Boot.ini 文件部分。 但是，当您在其他启动条目上启用 EMS，你不必添加**重定向 =** 再次参数。 等中的所有条目\[启动加载器\]部分中，**重定向 =** (并**redirectbaudrate =)** 适用于计算机上的所有启动项。

以下的 Bootcfg 命令的第二个启动项目上启用 EMS。 由于已设置的端口和波特率速率，有没有 **/port**或 **/baud**开关在命令中。

```command
bootcfg /ems ON /id 2
```

若要更改端口和波特率率设置，请使用 Bootcfg **/ems**开关和编辑参数。 以下命令更改为 COM1 的 EMS 端口，并更改为 57,600 Kbps 的波特率。

```command
bootcfg /ems EDIT /port COM1 /baud 57600
```

若要禁用 EMS 上的启动项，请使用 Bootcfg **/ems**开关和 OFF 参数。 以下命令禁用 EMS 上的第一个启动项目。

```command
bootcfg /ems OFF /id 1
```

如果未在任何其他的启动项目启用 EMS，Bootcfg 还会删除中的 EMS 端口和波特率率设置\[启动加载器\]Boot.ini 文件部分。

## <a name="changing-ems-settings-on-a-computer-running-windows-server-2008"></a>更改运行 Windows Server 2008 的计算机上的 EMS 设置

在 EMS 配置具有 ACPI BIOS 固件和 ACPI SPCR 表的计算机上的启动项上时，可以使用[ **BCDEdit /emssettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--emssettings)命令，并指定**BIOS**选项或**emsport**并**emsbaudrate**选项。 如果您使用**BIOS**选项，未设置**emsport**或**emsbaudrate**选项。

当在 EFI 固件的计算机上配置 EMS 或使用 ACPI BIOS 固件和不 ACPI SPCR 表，可以使用**BCDEdit /emssettings**命令并指定**emsport**并**emsbaudrate**选项。

**Emsport**并**emsbaudrate**选项设置为 EMS 控制台重定向的串行端口和传输速率。 这些设置适用于计算机上的所有启动项。 若要使用**emsbaudrate**，则还必须设置**emsport**选项。 默认情况下，传输速率设置为 9600 (9600 Kbps)。

例如，以下命令更改为 COM2 的 EMS 端口并更改为 57,600 Kbps 的波特率。

```command
bcdedit /emssettings EMSPORT:2 EMSBAUDRATE:57600
```

若要启用或禁用 EMS 上的启动项，请使用[ **BCDEdit /ems** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--ems)命令。

例如，以下命令启用 EMS 上具有 {173075c9-2cb2-11dc-b426-001558c41f5c} 的标识符的特定启动项...

```command
bcdedit /ems {173075c9-2cb2-11dc-b426-001558c41f5c} on
```

若要禁用 EMS 上的当前启动项目，请使用以下命令。

```command
bcdedit /ems off
```

> [!NOTE]
> 每个启动项使用作为标识符的 GUID。 如果未指定标识符**BCDEdit**命令将修改当前操作系统启动项目。 如果指定的启动项，则与启动项关联的 GUID 必须括在大括号 **{}** 。 若要查看所有活动的引导条目的 GUID 标识符，请使用**bcdedit /enum**命令。