---
title: 用于启用 EMS 重定向的启动参数
description: 用于启用 EMS 重定向的启动参数
ms.assetid: b93fd580-0e1d-4b1e-8358-1c6ce7e2eb5e
keywords:
- 启动参数 WDK
- 启动项参数 WDK
- 紧急管理服务 WDK 启动参数
- EMS 重定向 WDK 启动参数
- 远程管理 WDK 启动参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 490e1b00f550164e9640149b80f5e52c27874a43
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384357"
---
# <a name="boot-parameters-to-enable-ems-redirection"></a>用于启用 EMS 重定向的启动参数

利用紧急管理服务 (EMS) 技术，即使服务器未连接到网络或其他标准远程管理工具，也可以远程控制服务器的选定组件。 对于 x86、x64 和基于 Itanium 的计算机，所有版本的 Windows Server 2003 操作系统都支持 EMS。

> [!NOTE]
> 本主题说明如何在运行 Windows Server 2003 的计算机上启用 EMS。 Windows Vista 或更高版本的 Windows 不支持本部分中所述的启动参数。
> 如果在带有 BIOS 固件的计算机上为 EMS 配置了启动项，启动加载程序会在 \[ \] 启动菜单上的友好名称后面追加一个带括号的短语。 但是，如果友好名称和带括号的短语一起超过70个字符，则启动加载程序会在启动菜单中省略括号中的短语。 若要还原括起来的短语，请缩短友好名称。

若要确定计算机是否具有 ACPI 固件，请使用设备管理器 (devmgmt.msc) 。 在设备管理器中，展开 " **计算机** " 节点。 在具有 ACPI 固件的计算机上，" **计算机** " 下的节点名称包括 Word、 **ACPI**。

## <a name="enabling-ems-on-a-computer-without-an-acpi-spcr-table-in-operating-systems-prior-to-windows-server-2008"></a>在 Windows Server 2008 之前的操作系统中不使用 ACPI SPCR 表在计算机上启用 EMS

若要在装有 BIOS 固件但没有 ACPI 串行端口控制台重定向 (SPCR) 表的计算机上启用 EMS 控制台重定向，请将 **重定向 = COM * * * x* ，并将 **redirectbaudrate =** 参数添加到 \[ Boot.ini 文件的启动加载器 \] 部分。 这些参数设置 EMS 控制台重定向的端口和传输速率。 使用为 BIOS 中的带外通信建立的相同端口和传输速率。 然后，将 [**/redirect**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200) 参数添加到启动项。

以下 Bootcfg 命令在列表中的第一个启动条目上启用 EMS 控制台重定向。 它为 COM2 设置端口，并将传输速率设置为每秒 115200 kb (Kbps) 。 这是管理员在 BIOS 中为带外端口设置的相同端口和波特率设置。

```command
bootcfg /ems ON /port COM2 /baud 115200 /id 1
```

以下 Bootcfg 显示了命令的结果。 新添加的参数以粗体显示。

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

下面的示例演示 Boot.ini 文件上的同一命令的结果。

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

## <a name="enabling-ems-on-a-computer-without-an-acpi-spcr-table-in-windows-server-2008"></a>在 Windows Server 2008 中的不使用 ACPI SPCR 的计算机上启用 EMS

若要在装有 BIOS 固件但没有 ACPI 串行端口控制台重定向 (SPCR) 表的计算机上启用 EMS 控制台重定向，请使用 [**BCDEdit/emssettings**](./bcdedit--emssettings.md) 命令设置 COM 端口和波特率。

这些参数设置 EMS 控制台重定向的全局端口和传输速率。 使用为 BIOS 中的带外通信建立的相同端口和传输速率。

然后，使用 [**BCDEdit/ems**](./bcdedit--ems.md) 命令为启动条目启用 ems。

以下命令将全局 EMS 重定向设置设置为使用 COM2 和波特率115200，并为指定的启动条目启用 EMS。

```command
bcdedit /emssettings EMSPORT:2 EMSBAUDRATE:115200
```

```command
bcdedit /ems {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

## <a name="enabling-ems-on-a-computer-with-an-spcr-table-in-operating-systems-prior-to-windows-server-2008"></a>在 Windows Server 2008 之前的操作系统中使用 SPCR 表在计算机上启用 EMS

若要在具有 ACPI BIOS 固件和 ACPI SPCR 表的计算机上启用 EMS，可以使用 **重定向 = USEBIOSSETTINGS** 参数或 **重定向 = COM * * * x* 和 **redirectbaudrate =** 参数。 然后，可以将 [**/redirect**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200) 参数添加到启动项。

下面的示例演示了 **重定向 = USEBIOSSETTINGS** 参数的用法。 以下 Bootcfg 命令在列表中的第一个启动条目上启用 EMS 控制台重定向。

```command
bootcfg /ems ON /port BIOSSET /id 1
```

以下 Bootcfg 显示了命令的结果。 新添加的参数以粗体显示。

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

下面的示例演示 Boot.ini 文件上的同一命令的结果。

```command
[boot loader]
timeout=1
default=multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect=USEBIOSSETTINGS
[operating systems]
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="EMS boot" /fastdetect /redirect
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="Windows Server 2003, Standard" /fastdetect
```

## <a name="enabling-ems-on-a-computer-with-an-spcr-table-in-windows-server-2008"></a>使用 Windows Server 2008 中的 SPCR 表在计算机上启用 EMS

若要在具有 ACPI BIOS 固件和 ACPI SPCR 表的计算机上启用 EMS，可以使用 [**BCDEdit/emssettings**](./bcdedit--emssettings.md) 并指定 **BIOS** 参数或 **emsport** 和 **emsbaudrate** 参数。 若要为启动条目启用 EMS，请使用 [**BCDEdit/ems**](./bcdedit--ems.md) 命令。

下面的示例演示如何使用 **BIOS** 参数。 以下 BCDEdit 命令在当前启动项目上启用 EMS 控制台重定向。

```command
bcdedit /emssettings bios
bcdedit /ems on
```

## <a name="enabling-ems-on-a-computer-with-efi-firmware-in-operating-systems-prior-to-windows-server-2008"></a>在 Windows Server 2008 之前的操作系统中使用 EFI 固件在计算机上启用 EMS

若要在具有 EFI 固件的计算机上启用 EMS，请使用 Bootcfg 将 [**/redirect**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200) 参数添加到启动项。 Windows 通过读取 SPCR 表在固件中查找带外端口及其设置，并为 EMS 控制台重定向使用相同的端口和速率。

以下 Bootcfg 命令在基于 Itanium 的计算机上启用 EMS 重定向。 它使用 Bootcfg **/ems** 开关和 ON 参数将 **/redirect** 参数添加到启动项。 **/Id**开关标识启动项。

```command
bootcfg /ems ON /id 1
```

以下显示了 EFI NVRAM 中的启动选项的 Bootcfg 显示了 Bootcfg 命令的结果。 第一个启动条目配置为加载启用了 EMS 控制台重定向的操作系统。

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

## <a name="enabling-ems-on-a-computer-with-efi-firmware-in-windows-server-2008"></a>使用 Windows Server 2008 中的 EFI 固件在计算机上启用 EMS

若要在具有 EFI 固件的计算机上启用 EMS，请使用 [**BCDEdit/ems**](./bcdedit--ems.md) 命令并指定启动项。 Windows 通过读取 SPCR 表在固件中查找带外端口及其设置，并为 EMS 控制台重定向使用相同的端口和速率。

以下命令在标识符为 {18b123cd-2bf6-11db-bfae-00e018e2b8db} 的指定启动项上启用 EMS 控制台重定向。

```command
bcdedit /ems {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

## <a name="changing-ems-settings-on-a-computer-with-bios-firmware-in-operating-systems-prior-to-windows-server-2008"></a>在 Windows Server 2008 之前的操作系统中使用 BIOS 固件的计算机上更改 EMS 设置

在单个启动条目上配置 EMS 时，请将 " **重定向 =** " 参数添加到 \[ Boot.ini 文件的 "启动加载程序" \] 部分。 但是，如果对其他启动条目启用 EMS，则无需再次添加 **重定向 =** 参数。 与启动加载器部分中的所有项一样 \[ \] ， **重定向 =** (和 **redirectbaudrate =) ** 适用于计算机上的所有启动项。

以下 Bootcfg 命令在第二个启动条目上启用 EMS。 由于端口和波特率已经设置，命令中没有 **/port** 或 **/baud** 开关。

```command
bootcfg /ems ON /id 2
```

若要更改端口和波特率设置，请使用带有 EDIT 参数的 Bootcfg **/ems** 开关。 以下命令将 EMS 端口更改为 COM1，并将波特率改为 57600 Kbps。

```command
bootcfg /ems EDIT /port COM1 /baud 57600
```

若要对启动条目禁用 EMS，请使用带有 OFF 参数的 Bootcfg **/ems** 开关。 以下命令在第一个启动条目上禁用 EMS。

```command
bootcfg /ems OFF /id 1
```

如果未在任何其他启动项目上启用 EMS，Bootcfg 还会从 \[ Boot.ini 文件的启动加载器部分中删除 ems 端口和波特率设置 \] 。

## <a name="changing-ems-settings-on-a-computer-running-windows-server-2008"></a>在运行 Windows Server 2008 的计算机上更改 EMS 设置

当你在具有 ACPI BIOS 固件和 ACPI SPCR 表的计算机上的启动条目上配置 EMS 时，可以使用 [**BCDEdit/emssettings**](./bcdedit--emssettings.md) 命令并指定 **BIOS** 选项或 **emsport** 和 **emsbaudrate** 选项。 如果使用 **BIOS** 选项，请不要设置 **emsport** 或 **emsbaudrate** 选项。

当你在具有 EFI 固件的计算机上配置 EMS，或使用 ACPI BIOS 固件而不使用 ACPI SPCR 表在计算机上配置 EMS 时，可以使用 **BCDEdit/emssettings** 命令并指定 **emsport** 和 **emsbaudrate** 选项。

**Emsport**和**EMSBAUDRATE**选项设置 EMS 控制台重定向的串行端口和传输速率。 这些设置适用于计算机上的所有启动项。 若要使用 **emsbaudrate**，还必须设置 **emsport** 选项。 默认情况下，传输速率设置为 9600 (9600 Kbps) 。

例如，以下命令将 EMS 端口更改为 COM2 并将波特更改为 57600 Kbps。

```command
bcdedit /emssettings EMSPORT:2 EMSBAUDRATE:57600
```

若要启用或禁用启动项上的 EMS，请使用 [**BCDEdit/ems**](./bcdedit--ems.md) 命令。

例如，以下命令对标识符为 {173075c9-2cb2-11dc-b426-001558c41f5c} 的特定启动项启用 EMS。

```command
bcdedit /ems {173075c9-2cb2-11dc-b426-001558c41f5c} on
```

若要对当前启动条目禁用 EMS，请使用以下命令。

```command
bcdedit /ems off
```

> [!NOTE]
> 每个启动项都使用 GUID 作为标识符。 如果未指定标识符，则 **BCDEdit** 命令会修改当前的操作系统启动项。 如果指定了启动目，则必须用大括号 { } 将与启动项关联的 GUID 括起来。 若要查看所有活动启动条目的 GUID 标识符，请使用 **bcdedit/enum** 命令。