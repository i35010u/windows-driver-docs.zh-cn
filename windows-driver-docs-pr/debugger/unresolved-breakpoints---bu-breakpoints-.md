---
title: " (bu 断点的未解析断点) "
description: " (bu 断点的未解析断点) "
keywords:
- 断点，延迟
- 延迟断点
- 断点、BP 与 BU
- 断点，未解析
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64b486dd064c9efab1f7297a7330c61c63c7a096
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803243"
---
# <a name="unresolved-breakpoints-bu-breakpoints"></a> (bu 断点的未解析断点) 


如果为尚未加载的例程名称设置了 [断点](using-breakpoints.md) ，则断点称为 *延迟* 的、 *虚拟* 的或 *未解析* 的断点。  (这些术语可以互换使用。 ) 未解析的断点不与模块的任何特定负载相关联。 每次加载新应用程序时，都会检查此例程的名称。 如果出现此例程，调试器将计算虚拟断点的实际编码地址并启用断点。

如果使用 **bu** 命令设置断点，断点将被自动视为未解析。 如果此断点在已加载的模块中，则该断点仍处于启用状态且正常工作。 但是，如果以后卸载并重新加载该模块，则此断点不会消失。 另一方面，使用 **bp** 设置的断点会立即解析为一个地址。

**Bp** 断点与 **bu** 断点之间有三个主要差异：

-   **最佳** 的断点位置始终转换为地址。 如果模块更改移动了用于设置 **bp** 断点的代码，则断点将保留在同一地址。 另一方面， **bu** 断点仍与符号值关联 (通常是符号加上所使用的偏移量) ，即使其地址发生更改，也会跟踪该符号位置。

-   如果在已加载的模块中找到 **bp** 断点地址，并且以后卸载该模块，则会从断点列表中删除该断点。 另一方面，在重复卸载和加载后， **bu** 断点会保持不变。

-   用 **bp** 设置的断点不保存在 WinDbg [工作区](using-workspaces.md)中。 用 **bu** 设置的断点保存在工作区中。

### <a name="span-idcontrolling_address_breakpoints_and_unresolved_breakpointsspanspan-idcontrolling_address_breakpoints_and_unresolved_breakpointsspancontrolling-address-breakpoints-and-unresolved-breakpoints"></a><span id="controlling_address_breakpoints_and_unresolved_breakpoints"></span><span id="CONTROLLING_ADDRESS_BREAKPOINTS_AND_UNRESOLVED_BREAKPOINTS"></span>控制地址断点和未解析的断点

在包含 **/d** 开关时，可以通过 [**Bp (设置断点)**](bp--bu--bm--set-breakpoint-.md)命令或 **bm.exe (设置符号断点)** 命令创建地址断点。 未解析的断点可通过 **bu (设置未解析的断点)** 命令，或在未包含 **/d** 开关时进行 **bm.exe** 命令。 禁用、启用和修改断点的命令适用于所有类型的断点。 显示断点列表的命令包括所有断点，并指示每个断点的类型。 有关这些命令的列表，请参阅 [控制断点的方法](methods-of-controlling-breakpoints.md)。

"WinDbg **断点** " 对话框显示所有断点，指示带有表示法 "u" 的未解析断点。 此对话框可用于修改任何断点。此对话框上的 " **命令** " 文本框可用于创建任何类型的断点;如果省略该类型，则将创建一个未解析的断点。 有关详细信息，请参阅 [编辑 |断点](edit---breakpoints.md)。 当你在 "WinDbg [反汇编" 窗口](disassembly-window.md) 或 " [源](source-window.md)" 窗口中使用鼠标设置断点时，调试器将创建一个无法解析的断点。

 

 





