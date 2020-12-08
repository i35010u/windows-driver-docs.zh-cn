---
title: 断点
description: 断点
keywords:
- 调试器引擎，断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51469f1fd1722064612fa64467a40d45dff7e760
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788889"
---
# <a name="breakpoints"></a>断点


[调试器引擎](introduction.md#debugger-engine)可以创建和监视目标中的断点。

引擎可以在目标中插入两种类型的断点：软件断点和处理器断点。

-   通过在断点位置修改处理器指令，将 *软件断点* 插入目标的代码中。 调试器引擎跟踪此类断点;它们对于在该位置读取和写入内存的客户端是不可见的。 当目标执行修改的指令时，将触发软件断点。

-   调试器引擎会将 *处理器断点* 插入目标的处理器。 处理器断点可由不同的操作触发，例如，在位置 (（例如软件断点) ）执行指令，或在断点位置读取或写入内存。 处理器断点的支持取决于目标计算机中的处理器。

断点的地址可以通过显式地址、计算结果为地址的表达式或在以后计算为地址的表达式来指定。 在最后一种情况下，每次在目标中加载或卸载模块时，引擎将尝试重新计算该表达式，并在它可以确定地址时插入断点。这样，就可以在加载模块之前在模块中设置断点。

可以将多个参数与断点关联来控制其行为：

-   断点可以与目标中的特定线程关联，并将仅由该线程触发。

-   断点可以有与之关联的调试器命令;触发断点时，将自动执行这些命令。

-   在目标向其传递指定次数后，断点才能标记为非活动状态。

-   在第一次触发断点时，可以自动将其删除。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关使用断点的详细信息，请参阅 [使用断点](setting-breakpoints.md)。

 

 





