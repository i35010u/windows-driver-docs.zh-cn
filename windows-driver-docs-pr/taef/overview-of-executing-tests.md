---
title: 执行测试概述
description: 执行测试概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1643cdbc5660d1de5b72480513c2889053eaf3bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785097"
---
# <a name="overview-of-executing-tests"></a>执行测试概述

若要使用 TAEF 执行测试，请使用命令 **TE.EXE** 指定测试文件，该命令位于%： \Program Files (x86) \windows Kits\10\Testing\Runtimes\TAEF. 中。 例如，若要在 **CPP.Basic.Examples.dll** 测试文件中运行所有测试，请运行：

``` syntax
TE.exe CPP.Basic.Examples.dll
```

可以指定多个测试文件，即使它们包含以不同方式标记的测试。 例如，以下命令将运行 **CPP.Basic.Examples.dll** 中的所有测试和 **CSharp.Basic.Examples.dll** 文件，即使它们是用不同语言编写的：

``` syntax
TE.exe CPP.Basic.Examples.dll CSharp.Basic.Examples.dll
```

你还可以使用通配符来选择要执行的文件：

``` syntax
TE.exe *.Examples.dll
```

还可以指定相对路径：

``` syntax
TE.exe Examples\*
```

如果在命令提示符处指定的文件不包含任何测试，则 TE.exe 会报告一条错误消息。

## <a name="order-of-execution"></a>执行顺序

在命令提示符下指定的测试文件将按指定的顺序进行处理。

## <a name="out-of-process-execution"></a>进程外执行

默认情况下，TAEF 在进程外执行测试。 TAEF 使用 **TE.ProcessHost.exe** 进程来运行测试。 这使得测试可以彼此隔离，从而防止测试受到之前的测试的影响。 若要在 **TE.exe** 过程中执行测试，请为 **TE.exe** 指定 **"/inproc"** 选项。

## <a name="selecting-tests"></a>选择测试

您可以使用 **"/select"** 选项并指定 "选择查询" 来选择特定测试。 如果只想根据测试的名称进行选择，请改用 **"/name"** 选项。 有关如何使用选择查询来选择要执行的特定测试的详细信息，请参阅 [选择](selection.md)。

## <a name="specifying-part-of-command-as-environment-variable-te_cmd"></a>将部分命令指定为环境变量： **te \_ cmd**

如果 te.exe 的某些命令选项将始终相同，则可以利用环境变量 **te \_ cmd**。 无论将哪个 te \_ cmd 设置为，都将在命令后面追加 te.exe 执行。 对于 "*set te \_ cmd =/list*"，你将始终看到一列测试，就像在命令提示符处指定的二进制文件的执行。

## <a name="listing-tests"></a>列出测试

将 **"/list"** 命令选项与测试文件一起指定将在控制台的测试文件中列出类的名称和测试方法。 请注意，这只会列出每个指定二进制文件的二进制、类和测试方法的名称，而不会执行这些方法。 如果要列出更多详细信息，如设置和清理方法、每个级别指定的元数据或属性，并且在数据驱动的测试中，提供的数据，请改用 **"/listproperties"** 命令选项。

## <a name="test-results"></a>测试结果

对于任何一般的测试用例，测试结果取决于验证调用是已成功还是失败。 可以在 ["验证"](verify.md)中找到可用的 api 和其他详细信息。 如果在测试过程中未发出验证调用，则测试结果将默认为随 TAEF 一起提供的日志订阅服务器的 "通过"。 创作测试时，可以选择指定 **"DefaultTestResult"** 显式。 有关更多详细信息，请参阅 [创作测试](authoring-tests.md) 。

## <a name="help---command-options"></a>Help-命令选项

通过指定 **"/？"** 查找所有可用命令选项的 explantions TE.exe 的选项。 有关详细说明，请参阅 [Te.exe 命令选项](te-exe-command-line-parameters.md)。
