---
title: 无法解析的断点 （bu 断点）
description: 无法解析的断点 （bu 断点）
ms.assetid: 2c97314b-3098-47a0-8f15-3b7d61c95529
keywords:
- 断点延迟
- 延迟的断点
- 断点，BU 与最佳实践
- 无法解析的断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3785ebbfeca3ecad0c04105c2abb9699be11d645
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383753"
---
# <a name="unresolved-breakpoints-bu-breakpoints"></a>无法解析的断点 （bu 断点）


如果[断点](using-breakpoints.md)设置为未加载的常规名称，请调用该断点*延迟*，*虚拟*，或*无法解析的*断点。 （这些条款是可互换使用。）无法解析的断点不与任何特定模块的负载相关联。 加载新的应用程序时，每次它会检查此例程的名称。 如果出现此例程，调试器将计算虚拟断点的实际编码的地址，并启用断点。

如果使用设置断点**bu**命令中，断点将自动将其视为未解决的。 如果在加载的模块中有此断点，断点仍处于启用状态，并可以正常工作。 但是，如果更高版本中卸载并重新加载模块，此断点不会不会消失。 另一方面，与设置断点**bp**立即解析为地址。

有三个主要区别**bp**断点并**bu**断点：

-   一个**bp**断点位置始终转换为一个地址。 如果模块更改的移动代码**bp**设置了断点，断点仍保持在相同的地址。 但是， **bu**断点仍与已使用的符号值 （通常是一个符号加上偏移量） 相关联，还会跟踪此符号的位置，即使其地址发生变化。

-   如果**bp**断点地址是位于已加载模块，并且如果该模块是更高版本中卸载，从断点列表中删除断点。 但是， **bu**重复的卸载和加载后保留断点。

-   使用设置的断点**bp**不会保存在 WinDbg[工作区](using-workspaces.md)。 使用设置的断点**bu**保存在工作区中。

### <a name="span-idcontrollingaddressbreakpointsandunresolvedbreakpointsspanspan-idcontrollingaddressbreakpointsandunresolvedbreakpointsspancontrolling-address-breakpoints-and-unresolved-breakpoints"></a><span id="controlling_address_breakpoints_and_unresolved_breakpoints"></span><span id="CONTROLLING_ADDRESS_BREAKPOINTS_AND_UNRESOLVED_BREAKPOINTS"></span>控制地址断点和未解析的断点

可以使用创建地址断点[**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令，或**bm （设置符号断点）** 命令时 **/d**开关是包含。 可用于创建未解析的断点**bu （设置无法解析断点）** 命令，或**bm**命令时 **/d**不包含开关。 禁用、 启用，并且修改断点的命令应用于所有种类的断点。 显示断点的列表的命令包括所有断点，并指示每个类型。 有关这些命令的列表，请参阅[控制断点方法](methods-of-controlling-breakpoints.md)。

WinDbg**断点**对话框的显示所有断点，指示无法解析的断点，带有表示法"u"。 此对话框可以用于修改任何断点。**命令**文本框中，在此对话框可用于创建任何类型的断点; 如果省略的类型，创建未解析的断点。 有关详细信息，请参阅[编辑 |断点](edit---breakpoints.md)。 当通过使用鼠标在 WinDbg 中设置断点[反汇编窗口](disassembly-window.md)或[源窗口](source-window.md)，未解析的断点，调试器创建。

 

 





