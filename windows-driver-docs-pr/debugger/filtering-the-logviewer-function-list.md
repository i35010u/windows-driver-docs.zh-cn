---
title: 筛选 LogViewer 函数列表
description: 筛选 LogViewer 函数列表
ms.assetid: 258da8c3-ab94-40bd-bfa5-344571d34428
keywords:
- 日志查看器，筛选日志查看器函数列表
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebe5fa697b9c32a7211140cd41d221807d55df3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567850"
---
# <a name="filtering-the-logviewer-function-list"></a>筛选 LogViewer 函数列表


## <span id="ddk_filtering_the_logviewer_function_list_dtoolq"></span><span id="DDK_FILTERING_THE_LOGVIEWER_FUNCTION_LIST_DTOOLQ"></span>


记录器通常捕获一些不需要分析的函数调用。 这些可以通过筛选出记录器时它会创建日志文件。 但是，此过程是不可逆的因此，通常最好允许所有函数的日志，并筛选日志查看器中的显示。

有几种方法来筛选出日志查看器中的函数调用：

-   在主视图区域中，单击它，或使用光标键选择一个函数。 （选择一个函数时，日志查看器概述了它以红色。）然后，按 DELETE 键，或右键单击并选择**隐藏**。 这将隐藏视图从该函数调用的所有实例。

-   选择**视图 |Api 显示**。 将出现一个对话框具有以下三个方面。 右侧是按字母顺序列出的所有函数，并在左侧是分类分组。 可以启用或禁用的任何函数显示通过选中或清除其名称左侧的框。

-   选择**视图 |模块显示**。 将出现一个对话框，您可以选择调用模块;将显示这些模块中调用这些函数。

-   选择**视图 |第一次仅级别调用**。 这将显示在左侧列中具有"d0"的调用。 通常是需要隐藏由其他记录的函数的函数调用。 (例如，它通常是不值得关注的**ShellExecuteEx**在执行其过程期间进行 30 次不同的注册表调用。)

 

 





