---
title: MB 分析日志
description: MB 分析日志
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: f089a0aac43a5f80c3b4b9bbdfc35c1537d2bc29
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250455"
---
# <a name="mobilebroadband-analyzing-logs"></a>MobileBroadband 分析日志

[TextAnalysisTool](https://github.com/TextAnalysisTool/Releases) 是一种广泛的文本筛选工具，适用于具有大量 ETW 提供程序的复杂跟踪。 你可以使用 tat 文件筛选感兴趣的日志。

若要收集日志，请按照 [MobileBroadband 收集日志](mb-collecting-logs.md)中的步骤进行操作。

使用特定功能中包含的 tat 筛选器来筛选日志：

```
*  Copy and paste the lines into a <name>.tat file
*  Open the log of interest in TextAnalysisTool
*  Load the filter file(<name>.tat) into TextAnalysisTool by clicking File > Load Filters
```