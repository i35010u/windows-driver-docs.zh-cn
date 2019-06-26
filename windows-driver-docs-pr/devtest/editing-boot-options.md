---
title: 编辑启动选项
description: 编辑启动选项
ms.assetid: b50b3ac8-154a-4c26-907f-11e274a5c7c8
keywords:
- 启动选项 WDK，编辑
- 编辑启动选项
- Bootcfg 工具
- 自定义启动选项 WDK
- 启动项 WDK
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: a2857a69cc88ed1e51836bc85abdeeb2d756b805
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371386"
---
# <a name="editing-boot-options"></a>编辑启动选项


## <span id="ddk_editing_boot_options_tools"></span><span id="DDK_EDITING_BOOT_OPTIONS_TOOLS"></span>


本部分是编辑运行 Windows 10、 Windows 8、 Windows Server 2012、 Windows 7 或 Windows Server 2008 的计算机上的启动选项的实践指南。 建议用于自定义启动选项的基本元素的分步过程。

本部分介绍使用 BCDEdit，随操作系统附带的工具的方法。 有关 BCDEdit 命令语法的信息，请键入**bcdedit /？** 或**bcdedit /？主题**在命令提示符窗口中。 请参阅[BCD 启动选项参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)有关详细信息。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

有关编辑引导条目参数来启用和禁用 Windows 功能的帮助，请参阅[使用引导参数](using-boot-parameters.md)。

在启动选项中配置操作系统功能：

- [添加新的启动项](adding-boot-entries.md)通过复制现有的启动项目中相同的操作系统的操作系统。

- [更改友好名称](changing-the-friendly-name-of-a-boot-entry.md)新创建的启动项，以便您可以在启动菜单中识别它。

- [将参数添加到启动条目](changing-boot-parameters.md)的启用和配置 Windows 功能。

然后，若要使测试更快、 更轻松：

- [将新的启动项目的默认条目](changing-the-default-boot-entry.md)。

-  [更改引导菜单超时](changing-the-boot-menu-time-out.md)。因此，Windows 启动快速，可以缩短引导菜单超时。 或者，延长引导菜单超时，这样您有足够时间选择首选的启动项。

> [!CAUTION]
> 若要使用 BCDEdit 修改 BCD，所需管理权限。 更改某些启动项选项使用**BCDEdit /set**命令可能导致您的计算机无法运行。 或者，使用系统配置实用程序 (MSConfig.exe) 更改启动设置。
