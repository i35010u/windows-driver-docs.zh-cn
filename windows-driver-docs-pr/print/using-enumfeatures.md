---
title: 使用 EnumFeatures
description: 使用 EnumFeatures
keywords:
- EnumFeatures
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b32f8402c847f66dc9f1718bd2697c06a50bfc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835453"
---
# <a name="using-enumfeatures"></a>使用 EnumFeatures





调用方可以使用 **EnumFeatures** 检索包含当前受支持的驱动程序功能和所有 PPD 功能的关键字列表，其中，Pscript 将其视为 PPD \* OpenUI/ \* CloseUI 结构关键字中定义的功能：

\*LeadingEdge

\*UseHWMargins

Pscript 以特殊方式处理某些功能。 如果 \* 某个 PPD 中显示有多个 "解析"、" \* SetResolution" 和 " \* JCLResolution" 关键字，则将它们合并为一个标准功能。 合并后，如果 JCLResolution 首先出现，则功能的关键字名称将为 "JCLResolution" \* ; 否则为 "解决"。

**注意**   某些驱动程序功能 (例如% 镜像) 始终受支持，而其他驱动程序功能仅在某些条件下受支持。 例如，如果在 Windows 2000 和更高版本的操作系统版本上禁用了后台处理程序 EMF 假脱机功能，则将不支持% PageOrder 功能。 这些不受支持的驱动程序功能将不会显示在 **EnumFeatures** 的 "输出关键字" 列表中。

 

对于驱动程序功能，将在输出中包含关键字前缀 "%"。 对于 PPD 功能，关键字前缀 " \* " 不包含在输出中。

 

 




