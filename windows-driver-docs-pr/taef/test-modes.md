---
title: 测试模式
description: 测试模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f524cb76bee5bc62022806326f69881548b7cec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796391"
---
# <a name="test-modes"></a>测试模式


TAEF 提供了几种测试模式，可通过多种方式修改测试执行行为。 在继续此部分之前，请确保熟悉 TAEF 的基本执行，请参阅 [创作测试](authoring-tests.md) 和 [执行测试](executing-tests.md)。

**注意：** 测试模式彼此不兼容;在给定的测试运行过程中，只能启用一种测试模式。

以下测试模式当前由 TAEF 提供：

-   [圈](#loop)
-   [施加](#stress)

## <a name="span-idloopspanspan-idloopspanloop-test-mode"></a><span id="loop"></span><span id="LOOP"></span>循环测试模式


"循环测试模式" 提供了一种简单的功能，用于迭代单个测试或整个测试运行。 循环测试模式非常适合用于验证测试自动化的可靠性，或获取简单的压力或长距离自动化。

循环测试模式通过指定/testmode： loop 命令选项来启用。 还有其他两个可选参数，用于控制特定行为：

<span id="_Loop__loopNum_"></span><span id="_loop__loopnum_"></span><span id="_LOOP__LOOPNUM_"></span>/Loop： &lt; loopNum&gt;  
控制 (默认值： 1) 执行整个运行的次数。

<span id="_LoopTest__loopTestNum_"></span><span id="_looptest__looptestnum_"></span><span id="_LOOPTEST__LOOPTESTNUM_"></span>/LoopTest： &lt; loopTestNum&gt;  
控制 (默认值： 10) 执行运行中每个测试的次数。

下面的关系图显示了 TAEF 如何表示一个测试运行，其中包含一个测试文件，其中包含一个测试类，其中包含两个测试方法：

!["looptest" 参数](images/looptestmode-looptest.png)

关系图上的箭头显示 TAEF 下的执行流;显示 TAEF 如何执行安装装置，然后测试自身，以及在测试完成后将执行适当的清理装置。 "Looptest" 值会导致 TAEF 循环访问测试方法，这是 *最小的可能范围*。 请注意， **不** 会执行测试的设置和清理。 对于数据驱动的测试，也会出现相同的行为： "looptest" 值控制在 "测试方法" 级别的循环。

有些情况下，不可能只循环使用测试方法，这就是可以使用 "loop" 参数的地方。 下面的关系图显示了 TAEF 如何表示包含一个测试文件的测试运行，每个文件都包含一个测试类，每个测试类都包含一个测试方法：

!["loop" 参数](images/looptestmode-loop.png)

"Loop" 参数控制在 *可能的最大范围内* 循环;整个运行。 如果指定一个要 Te.exe 的测试文件，或者有多个测试文件，则整个运行将按指定的次数循环。

## <a name="span-idstressspanspan-idstressspanstress-test-mode"></a><span id="stress"></span><span id="STRESS"></span>压力测试模式


TAEF 的 "压力" 测试模式可帮助用户在 "压力" 环境下运行测试。 通过 "/testmode：压力" 命令选项启用压力测试模式，会启用以下行为：

1.  *Te.exe 无限期运行* -Te.exe 需要将 Ctrl + C 发送到命令提示符，或发送 \_ 到其隐藏窗口的一条 WM 关闭消息停止。
2.  *Te.exe 循环访问它所运行的测试的第一个 "组"* ，以避免在运行时加载后续文件，Te.exe 将循环访问它运行的测试的第一个 "组"。 请注意：
    1.  如果在命令提示符处指定多个测试文件，但没有选择任何内容，则只会执行第一个测试文件。
    2.  如果在命令提示符处指定了多个测试文件以及一个选择查询，则只会执行第一个测试文件中满足选择条件的测试。
    3.  如果在模块级别指定了数据驱动的测试文件，则执行的数据驱动参数的第一组合将会循环。

3.  *启用 "压力记录器"* -为了最大程度地减少日志记录所使用的资源量，Te.exe 切换到最小输出记录器：
    -   仅将错误写入控制台-不会写出其他日志项。
    -   每隔60秒，记录器会将当前通过/失败计数输出到控制台。
    -   每隔一秒，记录器都将输出一个 "."，以显示 Te.exe 仍在运行。

在压力测试模式下运行时，还需要指定 "/inproc" 开关-这意味着所有的压力执行都在 Te.exe 进程中运行。 此限制无需 TAEF 启动和维护单独的沙盒进程来执行，从而最大程度地减少因内存分配失败引起的测试失败。

 

 





