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
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77f0cb3bd7bb87c22721bbbe76f598697e3c9e9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525009"
---
# <a name="editing-boot-options"></a>编辑启动选项


## <span id="ddk_editing_boot_options_tools"></span><span id="DDK_EDITING_BOOT_OPTIONS_TOOLS"></span>


本部分是编辑运行 Windows 10、 Windows 8、 Windows Server 2012、 Windows 7 或 Windows Server 2008 的计算机上的启动选项的实践指南。 建议用于自定义启动选项的基本元素的分步过程。

本部分介绍使用 BCDEdit，随操作系统附带的工具的方法。 有关 BCDEdit 命令语法的信息，请键入**bcdedit /？** 或**bcdedit /？主题**在命令提示符窗口中。 请参阅[BCD 启动选项参考](https://msdn.microsoft.com/library/windows/hardware/ff542205)有关详细信息。

**请注意**  之前设置可能需要禁用或暂停 BitLocker 和安全启动的计算机上的 BCDEdit 选项。

 

有关编辑引导条目参数来启用和禁用 Windows 功能的帮助，请参阅[使用引导参数](using-boot-parameters.md)。

在启动选项中配置操作系统功能：

-   [添加新的启动项](adding-boot-entries.md)通过复制现有的启动项目中相同的操作系统的操作系统。

-   [更改友好名称](changing-the-friendly-name-of-a-boot-entry.md)新创建的启动项，以便您可以在启动菜单中识别它。

-   [将参数添加到启动条目](changing-boot-parameters.md)的启用和配置 Windows 功能。

然后，若要使测试更快、 更轻松：

-   [将新的启动项目的默认条目](changing-the-default-boot-entry.md)。

-   [更改引导菜单超时](changing-the-boot-menu-time-out.md)。因此，Windows 启动快速，可以缩短引导菜单超时。 或者，延长引导菜单超时，这样您有足够时间选择首选的启动项。

 

 





