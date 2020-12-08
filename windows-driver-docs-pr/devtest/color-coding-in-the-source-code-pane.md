---
title: 源代码窗格中的颜色编码
description: 源代码窗格中的颜色编码
keywords:
- 颜色编码 WDK 静态驱动程序验证程序
- 静态驱动程序验证器报表 WDK，源代码窗格
- 源代码窗格 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0108f649f3cea64cda59a8c6f6081218d5acbd2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795091"
---
# <a name="color-coding-in-the-source-code-pane"></a>源代码窗格中的颜色编码


SDV 使用颜色编码来帮助你快速识别代码源。

-   *背景色* 可帮助您确定您正在查看的文件的类型。

-   *文本颜色* 提供有关文件中代码的信息。

-   *蓝色突出显示* 指示与 "**跟踪树**" 窗格中所选元素关联的源代码行。 仅当在 " **跟踪树** " 窗格中选择了某个元素时，它才会出现。

### <a name="span-idbackground_colorsspanspan-idbackground_colorsspanbackground-colors"></a><span id="background_colors"></span><span id="BACKGROUND_COLORS"></span>背景色

" **源代码" 窗格** 包含两种背景色：黄色和白色。

-   **黄色**：指示驱动程序中的源代码，如 C 文件、头文件和库文件。

-   **白色**：指示 SDV 中的源代码。 这包括 [ () 的规则文件 ](static-driver-verifier-rule.md) 和操作系统模型文件 Sdv。

### <a name="span-idtext_colorsspanspan-idtext_colorsspantext-colors"></a><span id="text_colors"></span><span id="TEXT_COLORS"></span>文本颜色

以下文本颜色在 " **源代码** " 窗格中使用：

-   **绿色：** 提出.

-   **红色：** 在规则冲突的路径中执行的代码。

-   **黑色：** 未在规则冲突的路径中执行的代码。

-   **Blue：** 仅 (规则源文件)  (。 \* ) 指示未在规则冲突路径中执行的代码。

 

 





