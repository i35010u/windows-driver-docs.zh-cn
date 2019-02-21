---
title: 了解跟踪查看器
description: 了解跟踪查看器
ms.assetid: 2b839e7f-770f-4bf4-96e1-98524768f4f0
keywords:
- Static Driver Verifier 报表 WDK、 缺陷查看器
- 缺陷的查看器 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd007d9372688d1cb3b043de1f349c971a7f8c0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546695"
---
# <a name="understanding-the-trace-viewer"></a>了解跟踪查看器


当 SDV 检测到的验证选定的规则的至少一个规则冲突，跟踪查看器才可用。

跟踪查看器包含三个窗口。

-   [跟踪树窗格](trace-tree-pane.md)

-   [源代码窗格](source-code-pane.md)

-   [状态窗格](state-pane.md)

下面的屏幕截图显示了在缺陷查看器窗口和其跟踪树，源代码。

![缺陷查看器窗口和其跟踪树、 源代码和结果窗格的屏幕截图](images/sdv-defectviewerlabeled.png)

SDV 自动协调在三个缺陷查看器窗口中的显示。 例如，如果选择源代码元素中的**跟踪树**窗格中，SDV 自动将光标移到相应行中的代码**源代码**窗格 （反之亦然）。

同样，如果源代码中选择的元素**跟踪树**或**源代码**窗格更改的值的变量的 SDV 监视，这些更改会自动出现在**状态**窗格。

 

 





