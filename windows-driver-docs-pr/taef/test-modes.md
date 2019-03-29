---
title: 测试模式
description: 测试模式
ms.assetid: 1E9C0198-8C74-4966-A401-329723B5A933
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 809ac9a50cceb7405f25a3319253addb0114db8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577528"
---
# <a name="test-modes"></a>测试模式


TAEF 提供了多种测试模式对其进行修改以各种方式测试执行行为。 请确保您熟悉基本的 TAEF 执行，请参阅[创作测试](authoring-tests.md)并[执行测试](executing-tests.md)，然后继续进行本部分中。

**注意：** 测试模式不兼容;可能在给定测试运行期间启用只能有一个测试模式。

由 TAEF 目前提供以下测试模式：

-   [Loop](#loop)
-   [压力](#stress)

## <a name="span-idloopspanspan-idloopspanloop-test-mode"></a><span id="loop"></span><span id="LOOP"></span>循环测试模式


"循环测试模式"提供了用于循环访问各个测试的简单功能或整个测试运行。 循环测试模式非常适合用于验证测试自动化的可靠性，或获取简单的负载过大或长期持续自动化。

通过指定 /testmode:loop 命令选项启用循环测试模式。 有两个其他可选的参数的特定行为进行控制：

<span id="_Loop__loopNum_"></span><span id="_loop__loopnum_"></span><span id="_LOOP__LOOPNUM_"></span>/Loop:&lt;loopNum&gt;  
控件的整体运行的次数是执行 (默认值： 1)。

<span id="_LoopTest__loopTestNum_"></span><span id="_looptest__looptestnum_"></span><span id="_LOOPTEST__LOOPTESTNUM_"></span>/ LoopTest:&lt;loopTestNum&gt;  
控件中运行的每个测试获取多少次执行 (默认值： 10)。

关系图中，下面显示了如何 TAEF 表示测试运行的单个测试文件，其中包含单个测试类，其中包含两个测试方法组成：

![looptest 参数](images/looptestmode-looptest.png)

在关系图上的箭头显示 TAEF; 下的执行流显示 TAEF 执行安装程序装置的方式，然后在测试本身，并适当的清除装置后执行的测试都完成。 Looptest 值将导致 TAEF 进行迭代测试方法本身-周围*最小的范围*。 请注意，设置和测试的清理**不是**执行。 太对于数据驱动的测试，发生相同的行为: looptest 值控制循环在测试方法级别。

有时间时不能只是测试方法中，围绕循环，这就是可以使用 loop 参数的位置。 关系图中，下面显示了如何 TAEF 表示测试运行的两个测试文件，其中包含单个测试类和包含一个测试方法的每个测试类的每个文件组成：

![loop 参数](images/looptestmode-loop.png)

在循环的 loop 参数控件*最大可能范围*; 整个运行。 如果指定单个测试文件到 Te.exe，或者有多个测试文件，则将指定的次数的循环运行整个。

## <a name="span-idstressspanspan-idstressspanstress-test-mode"></a><span id="stress"></span><span id="STRESS"></span>压力测试模式


TAEF 压力测试模式可帮助用户在强度环境中运行测试。 通过启用压力测试模式下通过"/ testmode:stress"启用命令选项，以下行为：

1.  *无限期地运行 Te.exe* -Te.exe 需要 Ctrl + C 将发送到命令提示符下或 WM\_关闭消息要发送到其隐藏的窗口以停止。
2.  *Te.exe 循环访问其运行的测试的第一个组上*-若要避免在运行时，加载后续文件 Te.exe 将循环访问其运行的测试的第一个组。 请注意：
    1.  如果指定多个测试文件在命令提示符处，而无需任何选择，将执行仅第一个测试文件。
    2.  如果在命令提示符处指定了多个测试文件，以及所选内容查询，将执行仅满足选择条件时在第一个测试文件中的测试。
    3.  如果指定了这是在模块级别数据驱动的测试文件，将循环执行的第一个数据驱动的参数组合。

3.  *已启用压力记录器*-为了最大程度减少资源量，将使用日志记录，Te.exe 切换到最少的输出记录器：
    -   仅将错误写入到控制台的任何其他日志项不写出。
    -   每隔 60 秒，记录器将输出到控制台当前的通过/失败计数。
    -   每秒记录器将输出一个 '。 以显示 Te.exe 仍然正常工作。

压力测试模式中运行时，还需要指定"/ inproc"开关-这意味着所有压力执行在 Te.exe 进程中都运行。 这一限制不再需要 TAEF 启动和维护单独的沙盒进程的执行，因此可尽量减少由于内存分配失败的测试失败。

 

 





