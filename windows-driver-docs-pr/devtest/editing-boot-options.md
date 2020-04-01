---
title: 编辑启动选项
description: 编辑启动选项
ms.assetid: b50b3ac8-154a-4c26-907f-11e274a5c7c8
keywords:
- 启动选项 WDK，编辑
- 编辑启动选项
- Bootcfg 工具
- 自定义启动选项 WDK
- 启动条目 WDK
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9d06f21d2b022a2ee8028e94d09b976388a8d542
ms.sourcegitcommit: a2d1c389f0f413cc967068cbde22a5598e5a5d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80516776"
---
# <a name="editing-boot-options"></a>编辑启动选项

本部分是在运行 Windows Server 2008、Windows Server 2012 或 Windows 7 或更高版本的计算机上编辑启动选项的实用指南。 它建议提供自定义启动选项基本元素的分步过程。

本部分介绍使用 BCDEdit （操作系统附带的工具）的方法。 有关 BCDEdit 命令语法的信息，请键入**bcdedit/？** 或**bcdedit/？** 命令提示符窗口中的主题。 有关详细信息，请参阅[BCDEdit 选项参考](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

有关编辑启动项参数以启用和禁用 Windows 功能的帮助，请参阅[使用启动参数](using-boot-parameters.md)。

配置启动选项中的操作系统功能：

- 通过从同一操作系统复制现有启动条目，为操作系统[添加新的启动条目](adding-boot-entries.md)。

- 更改新创建的启动项的[友好名称](changing-the-friendly-name-of-a-boot-entry.md)，以便可以在启动菜单中识别它。

- [向启动项添加参数，以](changing-boot-parameters.md)启用和配置 Windows 功能。

这样，可以更快、更轻松地进行测试：

- 将[新的启动条目设为默认条目](changing-the-default-boot-entry.md)。

-  [更改启动菜单](changing-the-boot-menu-time-out.md)超时。可以缩短启动菜单超时，以便 Windows 快速启动。 或者，将延长启动菜单超时，以便有充足的时间来选择首选的启动条目。

## <a name="related-topics"></a>相关主题 
 [BCDEdit 命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/bcdedit-command-line-options)

> [!CAUTION]
> 需要管理权限才能使用 BCDEdit 来修改 BCD。 使用 BCDEdit /set 命令更改某些启动项目选项可能导致计算机无法运行。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。
