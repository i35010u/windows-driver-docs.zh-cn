---
title: 控制面板要求
description: 控制面板要求
ms.assetid: ad700594-b58c-4f6c-b594-e880612923b7
keywords:
- 控件面板 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 351a02fab804eae8ca4aac99a5356b3b3bcb5830
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547605"
---
# <a name="control-panel-requirements"></a>控制面板要求


## <span id="ddk_control_panel_requirements_gg"></span><span id="DDK_CONTROL_PANEL_REQUIREMENTS_GG"></span>


显示控制面板的扩展的要求如下：

-   现有的属性页必须保持不变。 任何由 Microsoft 提供的属性页 (包括**设置**) 必须不是禁用、 修改、 删除或替换。

-   可以仅添加自定义属性页**高级属性**。 最高级别上展示的功能是经常访问的每个 Windows 系统中包含的功能。 由于 Windows 2000 和更高版本的操作系统版本支持多个显示器，则无法将自定义属性页添加到显示控件面板中设置的顶级属性页。

-   控制面板扩展必须能够与现有的 Windows 控制面板元素一起运行。

-   自定义属性页必须用一个图标以及文本名称标记。 为了防止与将来的操作系统或 shell 版本冲突，还必须包含第三方选项卡，除了页标签，（与公司的徽标） 图标或文本与供应商的名称。 例如，"Acme 视频控件"是可接受;不是"视频控件"。

-   必须初始化控制面板扩展，如果必要的硬件/驱动程序组合不存在。 如果随自定义控制面板扩展插件的显示硬件不存在，不应加载扩展。 同样，如果自定义属性页具有依赖于专用驱动程序扩展 （例如，不能保证出现在每个其他显示器驱动程序的扩展） 的功能，这些功能必须禁用其自身，或者不能在属性页加载时未安装必要的驱动程序。

-   控件面板扩展必须遵守**隐藏该监视器无法显示的模式**上的复选框**监视器**选项卡。如果选中复选框，则控件面板扩展不能显示不会枚举任何模式**EnumDisplaySettings** （Microsoft Windows SDK 文档中所述）。

-   控制面板状态必须存储在注册表中。 否 *.ini*允许文件。 由你 Control Panel 的扩展维护任何状态必须存储在注册表中，可通过 HKR INF 文件中访问中的软件密钥。

 

 





