---
title: 用于配置的 GDL 指令
description: 用于配置的 GDL 指令
ms.assetid: c7b3c364-06b2-4de8-9fe6-2c77d313a2f8
keywords:
- 指令 WDK GDL，配置指令
- 源文件 WDK GDL，配置指令
- 配置指令 WDK GDL
- 分析器 WDK GDL，指令
- 功能指令 WDK GDL
- Option 指令 WDK GDL
- 开关/用例指令 WDK GDL
- 默认指令 WDK GDL
- DefaultOption 指令 WDK GDL
- 约束指令 WDK GDL
- InvalidCombinations 指令 WDK GDL
- 配置 WDK GDL，指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950f183fcbeb5e4d28c69068c856dd6748372649
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566178"
---
# <a name="gdl-directives-for-configurations"></a>用于配置的 GDL 指令


GDL 具有指令定义和使用配置的。

GDL 包含以下配置指令：

-   **\*功能**定义与功能相关的配置参数。

-   **\*选项**定义一组可以分配给每个配置参数的允许状态。 这些允许状态称为*选项*。

-   **\*交换机**， **\*用例**，并**默认**建立依赖于指定的配置参数。

-   **\*DefaultOption**构造默认配置。

-   **\*约束**并 **\*InvalidCombinations**指定无效的配置。 如果遇到这些指令，GDL 分析器将尝试修改它们以创建有效 （或不受约束） 配置。

有关配置指令的详细信息，请参阅[GDL 配置](gdl-configurations.md)。

 

 




