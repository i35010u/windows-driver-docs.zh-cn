---
title: BCDEdit 选项参考
description: BCDEdit 选项参考
ms.assetid: 351f8bc3-a228-48a4-bda8-69ee8521a5d3
ms.date: 09/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: af2208c1ca62dc71a4cf94ec242d861c69d99435
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778781"
---
# <a name="bcdedit-options-reference"></a>BCDEdit 选项参考

*启动项参数*或 *启动参数*是可选的，表示配置选项的特定于系统的设置。 可以将启动参数添加到操作系统的启动项。 它们存储在启动配置数据 (BCD) 存储中。

本部分介绍与在基于 x86 和基于 x64 的处理器的计算机上开发、测试和调试驱动程序相关的 Windows 支持的 Windows 版本的启动选项。 可以将这些参数添加到 Windows 操作系统的启动条目。

> [!CAUTION]
> 需要管理权限才能使用 BCDEdit 来修改 BCD。 使用 BCDEdit /set 命令更改某些启动项目选项可能导致计算机无法运行。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。 有关详细信息，请参阅[如何在 Windows 10 中打开 MSConfig](https://support.microsoft.com/help/4026130/windows-how-to-open-msconfig-in-windows-10)。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="in-this-section"></a>在本节中

|主题|说明|
|--- |--- |
|[BCDEdit /bootdebug](bcdedit--bootdebug.md)|/Bootdebug boot 选项启用或禁用当前或指定的 Windows 操作系统启动项的启动调试。|
|[BCDEdit/bootsequence](bcdedit--bootsequence.md)|为启动管理器设置一次性启动顺序。 |
|[BCDEdit /dbgsettings](bcdedit--dbgsettings.md)|/Dbgsettings 选项设置或显示计算机的当前全局调试器设置。 若要启用或禁用内核调试器，请使用 BCDEdit/debug 选项。|
|[BCDEdit /debug](bcdedit--debug.md)|/Debug boot 选项启用或禁用与指定启动项或当前启动项关联的 Windows 操作系统的内核调试。|
|[BCDEdit/默认27000](bcdedit--default.md)| 设置启动管理器将使用的默认项。|
|[BCDEdit /deletevalue](bcdedit--deletevalue.md)|/Deletevalue 选项删除或删除启动项选项 (并从 Windows 启动配置数据存储 (BCD) ) 其值。 使用 BCDEdit/deletevalue 命令删除使用 BCDEdit/set 命令添加的选项。 测试和调试驱动程序时，可能需要删除启动项选项。|
|[BCDEdit/displayorder](bcdedit--displayorder.md)|设置启动管理器显示多重引导菜单的顺序。|
|[BCDEdit /ems](bcdedit--ems.md)|/Ems 选项启用或禁用指定操作系统启动条目 (EMS) 的紧急管理服务。|
|[BCDEdit /emssettings](bcdedit--emssettings.md)|/Emssettings 选项为计算机设置全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用/ems 选项。 对于任何启动项，/emssettings 选项不会启用或禁用 EMS。|
|[BCDEdit/enum](bcdedit--enum.md)|/Enum 命令 (BCD) 存储中列出启动配置数据中的条目。 |
|[BCDEdit/event](bcdedit--event.md)|/Event 命令启用或禁用指定启动项的远程事件日志记录。 |
|[BCDEdit/hypervisorsettings](bcdedit--hypervisorsettings.md)|/Hypervisorsettings 选项设置或显示系统的虚拟机监控程序调试器设置。 |
|[BCDEdit /set](bcdedit--set.md)|BCDEdit/set 命令在 Windows 启动配置数据存储 (BCD) 中设置启动项目选项值。 使用 BCDEdit /set 命令可配置特定的启动项目元素，如内核调试程序设置、内存选项或启用测试签名的内核模式代码或负载备用硬件抽象层 (HAL) 的选项和内核文件。 若要删除启动项目选项，请使用 BCDEdit/deletevalue 命令。|
|[BCDEdit/timeout](bcdedit--timeout.md)|设置启动管理器超时值。 |
|[BCDEdit/tooldisplayorder](bcdedit--toolsdisplayorder.md)|设置启动管理器显示 "工具" 菜单的顺序。 |

## <a name="see-also"></a>请参阅

[添加启动项](./adding-boot-entries.md)