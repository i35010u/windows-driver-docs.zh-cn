---
title: 源代码窗格中的颜色编码
description: 源代码窗格中的颜色编码
ms.assetid: 1bc3635b-31ed-4453-aaef-cd5aac637df2
keywords:
- 颜色编码 WDK Static Driver Verifier
- 静态驱动程序验证工具报表 WDK，源代码窗格
- 源代码窗格 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cf997c4d9268f5a1619f41233faa93630bdbd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343157"
---
# <a name="color-coding-in-the-source-code-pane"></a>源代码窗格中的颜色编码


SDV 使用颜色编码以帮助您快速识别代码源。

-   *背景色*可帮助您确定您正在查看的文件的类型。

-   *文本颜色*提供有关文件中的代码的信息。

-   一个*蓝色突出显示*指示的行中选择的元素与关联的源代码**跟踪树**窗格。 仅当选择某个元素中出现**跟踪树**窗格。

### <a name="span-idbackgroundcolorsspanspan-idbackgroundcolorsspanbackground-colors"></a><span id="background_colors"></span><span id="BACKGROUND_COLORS"></span>背景色

**源代码窗格**包括两个背景色、 黄色和白色。

-   **黄色**:指示该驱动程序，如 C 文件、 头文件和库文件中的源代码。

-   **白色**:指示 SDV 中的源代码。 这包括[规则文件 (.slic)](static-driver-verifier-rule.md)和操作系统模型文件，Sdv harness.c。

### <a name="span-idtextcolorsspanspan-idtextcolorsspantext-colors"></a><span id="text_colors"></span><span id="TEXT_COLORS"></span>文本颜色

使用以下文本颜色**源代码**窗格：

-   **绿色：** 备注。

-   **红色：** 规则冲突的路径中执行的代码。

-   **黑色：** 不执行规则冲突的路径中的代码。

-   **蓝色：**(规则源文件 (\*.slic) 仅。)指示不执行规则冲突的路径中的代码。

 

 





