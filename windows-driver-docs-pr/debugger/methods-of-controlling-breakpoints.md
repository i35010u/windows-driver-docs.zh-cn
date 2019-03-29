---
title: 断点控制方法
description: 断点控制方法
ms.assetid: 69de05e8-1b41-403a-a628-88da9528e1ab
keywords:
- 断点控制
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b74e0d81622a613334ca2548b69bbd6b231e4ef8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563035"
---
# <a name="methods-of-controlling-breakpoints"></a>断点控制方法


通过虚拟地址、 模块和例程偏移量或 （在源模式下） 的源文件和行号，可以指定断点的位置。 如果没有偏移量的例程上放置一个断点，断点将激活时输入该例程。

有几个其他种类的断点：

-   断点可以与某些线程相关联。

-   之前触发它时，断点可以启用固定的数量的传递地址。

-   触发时，断点可以自动发出特定命令。

-   可以在非可执行文件内存和监视对要读取或写入到该位置上设置断点。

如果你正在调试多个进程在用户模式下，断点的集合取决于当前进程。 若要查看或更改进程的断点，必须为当前进程中选择的过程。 有关当前进程的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

### <a name="span-idmethodsofcontrollinganddisplayingbreakpointsspanspan-idmethodsofcontrollinganddisplayingbreakpointsspandebugger-commands-for-controlling-and-displaying-breakpoints"></a><span id="methods_of_controlling_and_displaying_breakpoints"></span><span id="METHODS_OF_CONTROLLING_AND_DISPLAYING_BREAKPOINTS"></span>用于控制和显示断点的调试器命令

若要控制或显示断点，可以使用以下方法：

-   使用[ **bl （断点列表）** ](bl--breakpoint-list-.md)命令以列出现有断点和当前状态。

-   使用[ **.bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)命令以列出所有断点以及用来创建它们的命令。

-   使用[**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令以设置新断点。

-   使用[ **bu （设置无法解析断点）** ](bp--bu--bm--set-breakpoint-.md)命令以设置新断点。 使用设置的断点**bu**称为未解析的断点，则它们具有不同特征与使用设置的断点**bp**。 有关完整详细信息，请参阅[无法解析断点 (bu 断点)](unresolved-breakpoints---bu-breakpoints-.md)。

-   使用[ **bm （设置符号断点）** ](bp--bu--bm--set-breakpoint-.md)命令与指定的模式匹配的符号上设置新断点。 与设置断点**bm**将与地址相关联 (如**bp**断点) 如果 **/d**开关是包含; 它将无法解析 (如**bu**断点) 如果此开关不包括。

-   使用[ **ba （中断的访问权限）** ](ba--break-on-access-.md)命令以设置*处理器断点*，也称为*数据断点*。 遇到这些断点的内存位置写入到，当它读取，为代码中，执行时或内核 I/O 发生时触发。 有关完整详细信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。

-   使用[ **（清除断点） 的 bc** ](bc--breakpoint-clear-.md)命令可以永久地删除一个或多个断点。

-   使用[ **（禁用断点） 的 bd** ](bd--breakpoint-disable-.md)命令，以暂时禁用一个或多个断点。

-   使用[**是 （启用断点）** ](be--breakpoint-enable-.md)命令以重新启用一个或多个已禁用的断点。

-   使用[ **（断点重新编号） 的 b** ](br--breakpoint-renumber-.md)命令以更改现有断点的 ID。

-   使用[ **bs （更新断点命令）** ](bs--update-breakpoint-command-.md)命令以更改与现有断点关联的命令。

-   使用[ **bsc （更新条件断点）** ](bsc--update-conditional-breakpoint-.md)命令以更改现有的条件断点发生的条件。

在 Visual Studio 和 WinDbg 中，有多个用户界面元素，可以帮助控制以及显示断点。 请参阅[在 Visual Studio 中设置断点](setting-breakpoints-in-visual-studio.md)并[在 WinDbg 中设置断点](setting-breakpoints-in-windbg.md)。

每个断点具有名为与它关联的断点 ID 的十进制数。 此数字标识的各种命令中的断点。

### <a name="span-idbreakpointcommandsspanspan-idbreakpointcommandsspanbreakpoint-commands"></a><span id="breakpoint_commands"></span><span id="BREAKPOINT_COMMANDS"></span>断点的命令

在断点命中断点时自动执行的可以包含命令。 例如，以下命令在 MyFunction + 0x47 处中断，写入转储文件，然后继续执行。

```dbgcmd
0:000> bu MyFunction+0x47 ".dump c:\mydump.dmp; g" 
```

**请注意**  如果您正在控制用户模式下的调试程序与内核调试程序，请不要使用[ **g （转向）** ](g--go-.md)断点命令字符串中。 串行接口可能无法跟上使用此命令，并将不能返回到 CDB 中断。 有关这种情况的详细信息，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

 

### <a name="span-idnumberofbreakpointsspanspan-idnumberofbreakpointsspannumber-of-breakpoints"></a><span id="number_of_breakpoints"></span><span id="NUMBER_OF_BREAKPOINTS"></span>断点的数量

在内核模式下，可以使用最多 32 软件断点。 在用户模式下，可以使用任意数量的软件的断点。

支持的处理器断点数取决于目标处理器体系结构。

### <a name="span-idconditionalbreakpointsspanspan-idconditionalbreakpointsspanconditional-breakpoints"></a><span id="conditional_breakpoints"></span><span id="CONDITIONAL_BREAKPOINTS"></span>条件断点

可以设置断点仅在某些情况下触发。 有关这些种类的断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

 

 





