---
title: 了解跟踪查看器
description: 了解跟踪查看器
keywords:
- 静态驱动程序验证程序报表 WDK，缺陷查看器
- 缺陷查看器 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bffcd6392de283416d0c9152a81873ff1e55772
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838087"
---
# <a name="understanding-the-trace-viewer"></a>了解跟踪查看器


当 SDV 检测到为验证选择的规则至少发生一项规则冲突时，跟踪查看器将可用。

跟踪查看器包含三个窗口。

-   [跟踪树窗格](trace-tree-pane.md)

-   [源代码窗格](source-code-pane.md)

-   [状态窗格](state-pane.md)

下面的屏幕截图显示了缺陷查看器窗口及其跟踪树的源代码。

!["缺陷查看器" 窗口及其 "跟踪树"、"源代码" 和 "结果" 窗格的屏幕截图](images/sdv-defectviewerlabeled.png)

SDV 自动协调三个缺陷查看器窗口中的显示。 例如，如果在 " **跟踪树** " 窗格中选择一个源代码元素，SDV 会自动将光标移到 " **源代码** " 窗格中相应的代码行 (，反之亦然) 。

同样，如果在 **跟踪树** 或 " **源代码** " 窗格中选择的源代码元素更改了 SDV 监视的变量的值，则这些更改将自动显示在 " **状态** " 窗格中。

 

 





