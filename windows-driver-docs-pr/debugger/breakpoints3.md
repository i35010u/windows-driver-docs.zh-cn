---
title: 断点
description: 断点
ms.assetid: f805667c-7ee1-4f66-bfc5-7e3b90b35b86
keywords:
- 调试器引擎断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e23641346c89d6738936749a7650baa68ea5bb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564255"
---
# <a name="breakpoints"></a>断点


[调试器引擎](introduction.md#debugger-engine)可以创建和监视目标中的断点。

有两种类型的引擎可以将插入到目标的断点： 软件断点和处理器断点。

-   *软件断点*通过修改断点的位置处的处理器指令插入到目标的代码。 调试器引擎跟踪的此类断点;它们是对客户端读取和写入该位置的内存不可见。 当目标执行修改后的指令时触发软件断点。

-   *处理器断点*由调试器引擎插入到目标的处理器。 处理器断点可以触发通过不同的操作，例如，执行的指令的位置 （如软件断点），或读取或写入内存在断点的位置。 依赖于目标的计算机中处理器的处理器断点支持。

通过显式地址、 一个表达式，计算结果为地址，或可能在将来的时间计算为一个地址的表达式，可以指定断点的地址。 在最后一种情况下，每次加载或在目标中，卸载模块时引擎将尝试重新计算该表达式，它可以确定地址; 如果插入断点这样，可以在加载前在模块中设置断点。

多个参数可以与断点，以控制其行为相关联：

-   断点可以与目标中的特定线程相关联，并仅将由该线程触发。

-   断点可以有与它; 关联的调试器命令触发断点时，将自动执行这些命令。

-   断点可以标记为非活动状态，直到目标已通过其指定的次数。

-   断点可以会自动删除第一次触发它时。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关使用断点的详细信息，请参阅[使用断点](setting-breakpoints.md)。

 

 





