---
title: 用于配置的 GDL 指令
description: 用于配置的 GDL 指令
keywords:
- 指令 WDK GDL，配置指令
- 源文件 WDK GDL，配置指令
- 配置指令 WDK GDL
- 分析器 WDK GDL，指令
- 功能指令 WDK GDL
- Option 指令 WDK GDL
- Switch/Case 指令 WDK GDL
- 默认指令 WDK GDL
- DefaultOption 指令 WDK GDL
- 约束指令 WDK GDL
- InvalidCombinations 指令 WDK GDL
- 配置 WDK GDL，指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf0d1805101571b39ce5ee211205c6a8be954bfc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797023"
---
# <a name="gdl-directives-for-configurations"></a>用于配置的 GDL 指令


GDL 包含用于定义和使用配置的指令。

GDL 包含以下配置指令：

-   **\* 功能** 定义与功能相关的配置参数。

-   **\* 选项** 定义可以分配给每个配置参数的一组允许的状态。 这些允许的状态称为 " *选项*"。

-   **\* Switch**、 **\* Case** 和 **Default** 与指定的配置参数建立依赖关系。

-   **\* DefaultOption** 构造默认配置。

-   **\* 约束** 和 **\* InvalidCombinations** 指定了无效配置。 如果遇到这些指令，GDL 分析器将尝试对其进行修改，以创建有效的 (或不受约束的) 配置。

有关配置指令的详细信息，请参阅 [GDL 配置](gdl-configurations.md)。

 

 




