---
title: 筛选 LogViewer 函数列表
description: 筛选 LogViewer 函数列表
keywords:
- LogViewer，筛选 LogViewer 函数列表
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0522256001a1792bdfcb651b18c25cfb3f499e7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838199"
---
# <a name="filtering-the-logviewer-function-list"></a>筛选 LogViewer 函数列表


## <span id="ddk_filtering_the_logviewer_function_list_dtoolq"></span><span id="DDK_FILTERING_THE_LOGVIEWER_FUNCTION_LIST_DTOOLQ"></span>


记录器通常捕获一些不需要进行分析的函数调用。 它们可以在创建日志文件时由记录器筛选掉。 但是，此过程是不可逆的，因此，通常最好是允许记录所有函数，然后在 LogViewer 中筛选显示。

可以通过多种方式来筛选 LogViewer 中的函数调用：

-   在主查看区域中，通过单击或使用光标键来选择一个函数。  (当选择某个函数时，LogViewer 会以红色列出该函数。 ) 然后按 DELETE 键，或者右键单击并选择 " **隐藏**"。 这将从视图中隐藏该函数调用的所有实例。

-   选择 " **查看" |显示 Api**。 将出现一个对话框，其中包含三个区域。 右侧是所有函数的按字母顺序排列的列表，左侧是分类分组。 通过选中或清除其名称左侧的框，可以启用或禁用任何功能的显示。

-   选择 " **查看" |模块显示**。 将显示一个对话框，允许您选择调用模块;只会显示从这些模块调用的函数。

-   选择 " **查看" |第一级调用**。 这将只显示左列中包含 "d0" 的调用。 通常需要隐藏由其他记录函数所做的函数调用。  (例如，知道 **ShellExecuteEx** 在其执行过程中进行了三十个不同的注册表调用，通常并不重要。 ) 

 

 





