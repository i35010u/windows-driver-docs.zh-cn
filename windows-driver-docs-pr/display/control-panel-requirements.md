---
title: 控制面板要求
description: 控制面板要求
keywords:
- 控制面板 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e073f9315b0f61e1bb0dd454d32ae6e40bae4f4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810143"
---
# <a name="control-panel-requirements"></a>控制面板要求


## <span id="ddk_control_panel_requirements_gg"></span><span id="DDK_CONTROL_PANEL_REQUIREMENTS_GG"></span>


下面是对 "显示控制面板" 的扩展的要求：

-   现有属性页必须保持不变。 任何 Microsoft 提供的属性页 (包括 **设置**) 不得禁用、修改、删除或替换。

-   自定义属性页只能添加到 " **高级属性**" 下。 在顶层公开的功能是每个 Windows 系统中都包含的常用功能。 由于 Windows 2000 和更高版本的操作系统版本支持多个显示，因此不能将自定义属性页添加到 "显示" 控制面板中的顶级属性页集。

-   控制面板扩展必须能够在现有 Windows 控制面板元素上操作。

-   除了文本名称外，自定义属性页必须用图标标记。 为了防止与将来的操作系统或 shell 版本发生冲突，第三方选项卡除了包含页面标签外，还必须包含该公司徽标的图标 () 或带有供应商名称的文本。 例如，可以接受 "Acme 视频控件";"视频控件" 不是。

-   如果必需的硬件/驱动程序组合不存在，则控制面板扩展不能初始化。 如果自定义控制面板扩展附带的显示硬件不存在，则不应加载扩展。 同样，如果自定义属性页的功能取决于专用驱动程序扩展（例如，那些不能保证出现在所有其他显示器驱动程序中的扩展），则在没有安装必要的驱动程序时，这些功能必须自动禁用，或者属性页不得进行加载。

-   控制面板扩展必须遵守 "**监视**" 选项卡上的 "**此监视器无法显示的隐藏模式**" 复选框。如果选中该复选框，则 "控制面板" 扩展不得显示 "Microsoft Windows SDK 文档) 中所述的 (**EnumDisplaySettings** 未枚举的任何模式。

-   控制面板状态必须存储在注册表中。 不允许使用 *.ini* 文件。 你的控制面板扩展维护的任何状态都必须存储在注册表中的软件密钥中，并可通过 INF 文件中的 HKR 访问。

 

 





