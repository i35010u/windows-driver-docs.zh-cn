---
title: 静态工具和 CodeQL
description: 在 Windows 驱动程序源代码中使用静态工具和 CodeQL 来发现并修复任何被视为 Must-Fix 的问题
keywords:
- 动态验证工具 WDK
- 静态验证工具 WDK
ms.date: 12/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 11a09bb25b7896ebe25fa27581f3a9afbead9629
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124265"
---
# <a name="codeql-and-the-static-tools-logo-test"></a>CodeQL 和静态工具徽标测试

Microsoft 致力于缓解 Windows 操作系统的攻击面，并确保第三方驱动程序满足强安全块对于实现该目标至关重要。  Microsoft 将通过向 [Windows 硬件兼容计划](/windows-hardware/design/compatibility)添加新的要求来设置此安全栏。  此要求表明所有驱动程序提交必须对驱动程序源代码使用 [CodeQL](https://securitylab.github.com/tools/codeql) 引擎，并修复任何被视为 **"必须修复"** 的冲突。

Semmle 的[CodeQL](https://semmle.com/codeql)是一种强大的保护软件静态分析技术。 大范围的高价值安全查询和强大平台的组合使其成为确保第三方驱动程序代码安全的重要工具。

[静态工具徽标测试](/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae)将强制对驱动程序源代码进行分析并修复任何 **"必须修复"** 冲突。

本主题介绍如何执行以下操作：

- 使用 CodeQL 分析驱动程序源代码，以了解已知的严重影响安全问题。
- 确保静态工具徽标测试可以使用运行 CodeQL 的结果。
- 在 Windows 硬件兼容性计划中，确定哪些 **"必须修复"** [查询](#must-fix-queries) 必须运行而不会出现证书错误。

> [!IMPORTANT]
> 此信息是初步信息，并将在完成查询规则集分发时进行更新。
>

## <a name="concepts-for-codeql"></a>CodeQL 的概念

**CodeQL** 是开发人员用来执行安全分析的分析引擎。  **CodeQL 数据库** 是包含以下内容的目录：

- 从驱动程序源代码中提取的可查询数据。
- 用于直接在源代码中显示查询结果的源引用。  **查询** 可以视为 "检查" 或 "规则"。  每个查询都表示一个要搜索的不同安全漏洞。 有关详细信息，请参阅在 CodeQL 文档中 [编写查询](https://help.semmle.com/QL/learn-ql/writing-queries/writing-queries.html) 。
- 查询结果。
- 在数据库创建、执行查询和其他操作时生成的日志文件。

本主题详细介绍了如何使用 CodeQL CLI 执行分析，并专注于适用于 Windows 的驱动程序开发人员。  补充文档可在 [CodeQL 入门](https://help.semmle.com/codeql/codeql-cli/procedures/get-started.html)上找到。

我们将使用 [CodeQL 命令行工具 (CLI) ](https://help.semmle.com/codeql/codeql-cli.html) 从各种编译和解释语言创建 CodeQL 数据库，然后使用单独的查询和驱动程序特定的查询套件分析该数据库。

## <a name="codeql-windows-setup"></a>CodeQL Windows 安装程序

### <a name="download-install-and-test-codeql"></a>下载、安装并测试 CodeQL

1. 第一个任务是创建一个包含 CodeQL 的目录。  此示例将使用 `C:\codeql-home\`

```command
C:\> mkdir C:\codeql-home
```

2. 导航到 Github [CodeQL 下载页](https://github.com/github/codeql-cli-binaries/releases/)
3. 下载 zip 文件的最新版本。 例如，64位 Windows "codeql-win64.zip"。
4. 将下载的 zip 文件解压缩到目录，例如  `C:\codeql-home\codeql-win64` 。
5. 通过显示帮助确认 CodeCL 命令是否正常工作。

```command
C:\codeql-home\codeql-win64\codeql>codeql --help
Usage: codeql <command> <argument>...
Create and query CodeQL databases, or work with the QL language.

GitHub makes this program freely available for the analysis of open-source software and certain other uses, but it is
not itself free software. Type codeql --license to see the license terms.

      --license              Show the license terms for the CodeQL toolchain.
Common options:
  -h, --help                 Show this help text.
  -v, --verbose              Incrementally increase the number of progress messages printed.
  -q, --quiet                Incrementally decrease the number of progress messages printed.
Some advanced options have been hidden; try --help -v for a fuller view.
Commands:
  query     Compile and execute QL code.
  bqrs      Get information from .bqrs files.
  database  Create, analyze and process CodeQL databases.
  dataset   [Plumbing] Work with raw QL datasets.
  test      Execute QL unit tests.
  resolve   [Deep plumbing] Helper commands to resolve disk locations etc.
  execute   [Deep plumbing] Low-level commands that need special JVM options.
  version   Show the version of the CodeQL toolchain.
  generate  Generate formatted QL documentation.
```

### <a name="clone-the-repository-to-access-the-query-rules"></a>克隆存储库以访问查询规则

1. 导航到 [CodeQL Github 存储库](https://github.com/github/codeql)。

2. [克隆](https://github.com/git-guides/git-clone) 存储库以下载所需的 CodeQL 查询。

```command
C:\codeql-home\>git clone https://github.com/github/codeql.git
```

> [!NOTE]
> 使用 CodeQL 进行 WHCP 测试的目的是在 **[硬件实验室工具包下接受 ()](/windows-hardware/test/hlk/) 最终用户许可协议**。
> 在不久的将来，将更新上述说明中的步骤2，以指定包含仅包含驱动程序相关查询的查询套件的存储库。

此页假定为 Windows 开发环境，并且存储库将安装在 *C:\codeql-home* 下。

## <a name="building-your-codeql-database"></a>构建 CodeQL 数据库

接下来的步骤将创建一个可用于分析的 CodeQL 数据库。

创建目录以将 CodeQL 数据库保留 (数据库文件夹) 。  此示例将使用 *C:\codeql-home\databases*

```command
mkdir C:\codeql-home\databases
```

通常，用于创建 CodeQL 数据库的命令将如下所示：

```command
codeql database create -l=[cpp/csharp/python/java/javascript/go/xml] -s=<path to source code> -c=<command to build> <database folder>\<project name> -j 0
```

有关使用数据库 create 命令的帮助，请键入：

```command
codeql database create --help
```

CodeQl 使用 MSBuild 编译器来处理 c + + 代码，以便对其进行分析。

### <a name="example"></a>示例

使用用于生成驱动程序源代码的命令行环境（例如 [企业 Windows 驱动程序工具包 (EWDK) ](../develop/using-the-enterprise-wdk.md)）导航到克隆了存储库的 CodeQL 工具文件夹。

此示例将处理评估 github 上提供的 kmdfecho 驱动程序示例。

https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf

Kmdf 示例位于 `C:\codeql-home\drivers\kmdf` 。

运行以下命令，在 *C:\codeql-home\databases\kmdf* 下创建新的 CodeQL 数据库。

```command
C:\codeql-home>C:\codeql-home\codeql-win64\codeql\codeql database create -l=cpp -s=C:\codeql-home\drivers\kmdf -c "msbuild /t:rebuild "C:\codeql-home\drivers\kmdf\kmdfecho.sln" /p:UseSharedCompilation=false" "C:\codeql-home\databases\kmdf" -j 0
```

*"-J 0"* 标志指示使用的线程数与创建数据库的导入步骤中的 CPU 数量相同。

此示例使用此参数来查找和生成驱动程序项目。 Msbuild 命令必须在路径中可用。

```command
msbuild /t:rebuild "C:\codeql-home\drivers\kmdf\kmdfecho.sln"
```

## <a name="summary-of-directory-locations"></a>目录位置摘要

此时，在我们的示例设置中，将显示以下目录。

| 描述            | 位置                           |
|------------------------|------------------------------------|
| Codeql.exe             | C:\codeql-home\codeql-win64\codeql |
| C + + 规则              | C:\codeql-home\codeql\cpp          |
| 数据库              | C:\codeql-home\databases           |
| 待测试的驱动程序代码 | C:\codeql-home\drivers\kmdf        |

## <a name="perform-analysis"></a>执行分析

此时，设置已完成，下一步是对驱动程序源代码执行实际分析。

CodeQL CLI 工具可以对在上一步中创建的数据库进行分析，还可以运行查询或查询套件。  以 *CSV* 或 *SARIF* 格式报告发现的输出。

就本示例而言，假设要在驱动程序源代码上运行的查询套件是在克隆 CodeQL Microsoft 存储库时包含的套件。

要执行分析的数据库分析命令使用以下语法。

```command
codeql database analyze <database> <path to query, suite or directory> 
--search-path=<path to search for packages> 
--format=[csv/sarif-latest/sarifv1/sarifv2/sarifv2.1.0/graphtext/dgml] 
--output=<output file directory>\output file name> 
-j 0
```
*"-J 0"* 标志指示使用的线程数与分析部分中的 CPU 数量相同。

使用参数在 codeql 数据库分析命令中显示帮助 `--help` 。

```command
C:\codeql-home\codeql-win64\codeql>codeql database analyze --help
Usage: codeql database analyze [OPTIONS] <database> [<query|dir|suite>...]
Analyze a database, producing meaningful results in the context of the source code.

Run a query suite (or some individual queries) against a CodeQL database, producing results, styled as alerts or paths,
in SARIF or another interpreted format.

...

```

例如，若要对 kmdf 回显驱动程序的 TooFewArguments 查询进行评估，并使用 SARIF 格式返回的结果，请使用此命令。

```command
C:\codeql-home>C:\codeql-home\codeql-win64\codeql\codeql database analyze "C:\codeql-home\databases\kmdf" "C:\codeql-home\codeql\cpp\ql\src\Likely Bugs\Underspecified Functions\TooFewArguments.ql" --format=sarifv2.1.0 --output=C:\codeql-home\databases\kmdfecho1.sarif -j 0
```

应显示类似于以下内容的输出。

```command
Running queries.
Compiling query plan for C:\codeql-home\codeql\cpp\ql\src\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
[1/1 comp 21.5s] Compiled C:\codeql-home\codeql\cpp\ql\src\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
[1/1 eval 4.6s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Underspecified Functions\TooFewArguments.bqrs.
Shutting down query evaluator.
Interpreting results.
```

您可以使用 *"– timeout = [秒]"* 标志为整个操作指定超时。  这可用于分析查询，而不受单个长时间运行的查询的限制。  [数据库分析](https://help.semmle.com/codeql/codeql-cli/commands/database-analyze.html)中介绍了更多用于调整分析优化的选项。

目前，上面的命令演示了如何只运行一个查询 *"TooFewArguments. q"*。  可以通过在一个命令中按顺序列出所有查询来一次运行多个查询。  

在不久的将来，将提供包含所有相关驱动程序查询的特定于驱动程序的 *查询套件* 。 有关详细信息，请参阅 [查询套件](https://help.semmle.com/codeql/codeql-cli/procedures/query-suites.html)。

## <a name="troubleshooting"></a>疑难解答

对于数据库版本不匹配问题，下列工具可能有所帮助。

使用 "codeql 版本" 命令显示 codeql exe 的版本。

```command
C:\codeql-home\codeql-win64\codeql>codeql version
CodeQL command-line toolchain release 2.4.0.
Copyright (C) 2019-2020 GitHub, Inc.
Unpacked in: C:\codeql-home\codeql-win64\codeql
   Analysis results depend critically on separately distributed query and
   extractor modules. To list modules that are visible to the toolchain,
   use 'codeql resolve qlpacks' and 'codeql resolve languages'.
```

数据库升级命令将更新数据库。 请注意，这是一个单向升级，不可逆。 有关详细信息，请参阅 [数据库升级](https://help.semmle.com/codeql/codeql-cli/commands/database-upgrade.html)。

## <a name="queries"></a>查询

此页将会更新，以指示对于 WHCP 认证，哪些查询已被正式视为 **"必须修复"** 。

Microsoft 建议在 *所有* 驱动程序源代码上运行的查询包括：

| ID                       | 位置   |
| ------------------------ | ---------- |
| [cpp/参数太少](https://help.semmle.com/wiki/display/CCPPOBJ/Call+to+function+with+fewer+arguments+than+declared+parameters)   | *cpp/q/src/可能的 Bug/Underspecified 函数/TooFewArguments. q* |
| [cpp/additionoverflow-检查](https://help.semmle.com/wiki/display/CCPPOBJ/Bad+check+for+overflow+of+integer+addition)   | *cpp/q/src/可能的 Bug/算数/BadAdditionOverflowCheck. q* |
| [cpp/指针-overflowcheck](https://help.semmle.com/wiki/display/CCPPOBJ/Pointer+overflow+check)   | *cpp/q/src/可能的 Bug/内存管理/PointerOverflow. q* | 
| [cpp/hresult-booleanconversion](https://help.semmle.com/wiki/display/CCPPOBJ/Cast+between+HRESULT+and+a+Boolean+type)   | *cpp/q/src/Security/CWE/CWE-253/HResultBooleanConversion. q* | 
| [cpp/错误-typeconversion](https://help.semmle.com/wiki/pages/viewpage.action?pageId=29392920)   | *cpp/q/src/Security/CWE/CWE-704/WcharCharConversion. q* |
| [cpp/integermultiplication-强制转换为 long](https://help.semmle.com/wiki/display/CCPPOBJ/Multiplication+result+converted+to+larger+type)   | *cpp/q/src/可能的 Bug/算数/IntMultToLong. q* |
| [cpp/已签名-overflowcheck](https://help.semmle.com/wiki/display/CCPPOBJ/Signed+overflow+check)   | *cpp/q/src/可能的 Bug/算数/SignedOverflowCheck. q* |
| [cpp/向上转换-数组-pointerarithmetic](https://help.semmle.com/wiki/display/CCPPOBJ/Upcast+array+used+in+pointer+arithmetic)   | *cpp/q/src/可能的 Bug/转换/CastArrayPointerArithmetic。 q* |
| [cpp/withwider 类型](https://help.semmle.com/wiki/display/CCPPOBJ/Comparison+of+narrow+type+with+wide+type+in+loop+condition)   | *cpp/q/src/Security/CWE/CWE-190/ComparisonWithWiderType. q* |
| [cpp/可疑-添加-sizeof](https://help.semmle.com/wiki/display/CCPPOBJ/Suspicious+add+with+sizeof)   | *cpp/q/src/Security/CWE/CWE-468/SuspiciousAddWithSizeof q* |
| [cpp/request.form 函数](https://help.semmle.com/wiki/display/CCPPOBJ/Use+of+potentially+dangerous+function)   | *cpp/q/src/Security/CWE/CWE-676/PotentiallyDangerousFunction q* |
| [cpp/notoperator-用法](https://help.semmle.com/wiki/display/CCPPOBJ/Incorrect+%27not%27+operator+usage)   | *cpp/q/src/可能的 Bug/错误录入/IncorrectNotOperatorUsage。 q* | 
| [cpp/offset-beforerange-check](https://help.semmle.com/wiki/display/CCPPOBJ/Array+offset+used+before+range+check)  | *cpp/q/src/最佳方案/可能的错误/OffsetUseBeforeRangeCheck. q*   |
| [cpp/可疑-sizeof](https://help.semmle.com/wiki/display/CCPPOBJ/Suspicious+add+with+sizeof)   | *cpp/q/src/可能的 Bug/内存管理/SuspiciousSizeof. q* |
| [cpp/未初始化-本地](https://help.semmle.com/wiki/display/CCPPOBJ/Potentially+uninitialized+local+variable)   | *cpp/q/src/可能的 Bug/内存管理/UninitializedLocal. q* |
| [cpp/unterminatedvariadic-调用](https://help.semmle.com/wiki/display/CCPPOBJ/Call+to+function+with+fewer+arguments+than+declared+parameters)   | *cpp/q/src/Security/CWE/CWE-121/UnterminatedVarargsCall. q* |
| [cpp/可疑-pointerscaling](https://help.semmle.com/wiki/display/CCPPOBJ/Suspicious+pointer+scaling)   | *cpp/q/src/Security/CWE/CWE-468/IncorrectPointerScaling q* |
| [cpp/pointerscaling-void](https://help.semmle.com/wiki/display/CCPPOBJ/Suspicious+pointer+scaling+to+void)   | *cpp/q/src/Security/CWE/CWE-468/IncorrectPointerScalingVoid q* |
| [cpp/有条件-未初始化-变量](https://help.semmle.com/wiki/display/CCPPOBJ/Conditionally+uninitialized+variable)   | */cpp/ql/src/Security/CWE/CWE-457/ConditionallyUninitializedVariable.ql.* | 

### <a name="must-fix-queries"></a>Must-Fix 查询

下面的查询子集当前被视为 WHCP 认证的 **"必须修复"** 。  **此列表可能会更改**。  2021年4月1日，最终列表将发布到此页。  

| ID            | 位置   |
| ------------- | ---------- |
| [cpp/参数太少](https://help.semmle.com/wiki/display/CCPPOBJ/Call+to+function+with+fewer+arguments+than+declared+parameters)   | *cpp/q/src/可能的 Bug/Underspecified 函数/TooFewArguments. q* |
| [cpp/additionoverflow-检查](https://help.semmle.com/wiki/display/CCPPOBJ/Bad+check+for+overflow+of+integer+addition)   | *cpp/q/src/可能的 Bug/算数/BadAdditionOverflowCheck. q* |
| [cpp/指针-overflowcheck](https://help.semmle.com/wiki/display/CCPPOBJ/Pointer+overflow+check)   | *cpp/q/src/可能的 Bug/内存管理/PointerOverflow. q* |
| [cpp/hresult-booleanconversion](https://help.semmle.com/wiki/display/CCPPOBJ/Cast+between+HRESULT+and+a+Boolean+type)   | *cpp/q/src/Security/CWE/CWE-253/HResultBooleanConversion. q* | 
| [cpp/错误-typeconversion](https://help.semmle.com/wiki/pages/viewpage.action?pageId=29392920)   | *cpp/q/src/Security/CWE/CWE-704/WcharCharConversion. q* | 
| [cpp/有条件-未初始化-变量](https://help.semmle.com/wiki/display/CCPPOBJ/Conditionally+uninitialized+variable)   | */cpp/ql/src/Security/CWE/CWE-457/ConditionallyUninitializedVariable.ql.* | 
| [cpp/withwider 类型](https://help.semmle.com/wiki/display/CCPPOBJ/Comparison+of+narrow+type+with+wide+type+in+loop+condition)   | *cpp/q/src/Security/CWE/CWE-190/ComparisonWithWiderType. q* |
| [cpp/未初始化-本地](https://help.semmle.com/wiki/display/CCPPOBJ/Potentially+uninitialized+local+variable)   | *cpp/q/src/可能的 Bug/内存管理/UninitializedLocal. q* |

## <a name="view-analysis"></a>查看分析

在上一部分中运行分析命令的结果可以 [SARIF](https://help.semmle.com/codeql/glossary.html#sarif-results-file) 文件格式查看。  有关 SARIF 输出的详细信息，请参阅 [SARIF 概述](https://help.semmle.com/codeql/codeql-cli/reference/sarif-overview.html)。

SARIF 文件包含已运行的每个查询的 " **结果** " 部分，其中包含有关已完成分析的详细信息。  例如，如果查询发现一个漏洞，则 SARIF 文件将包含该漏洞的详细信息以及发现缺陷的位置的详细信息。 如果未找到任何漏洞，则结果部分将为空。

```xml
    "results" : [ ],
```

若要查看结果，请安装 [适用于 Visual Studio 的 MICROSOFT SARIF 查看器](https://marketplace.visualstudio.com/items?itemName=WDGIS.MicrosoftSarifViewer) 并按照该页上的说明进行操作。  或者，你可以 [为 Visual Studio Code 安装 SARIF 扩展](https://marketplace.visualstudio.com/items?itemName=MS-SarifVSCode.sarif-viewer)。

## <a name="driver-verification-log-dvl-consumption-of-sarif-output"></a>SARIF 输出的驱动程序验证日志 (DVL) 消耗

Microsoft 将强制要求在静态工具徽标测试中运行 CodeQL 查询。  静态工具徽标测试使用 [驱动程序验证日志 (DVL) ](../develop/creating-a-driver-verification-log.md) 从在驱动程序源代码上运行的不同静态分析中收集结果。  然后，将此 DVL 分析为在 HLK 测试中使用的静态工具徽标测试的一部分。

CodeQL 结果遵循相同的模型，该模型使用 DVL 来表明要认证的驱动程序运行了相应的 CodeQL 查询，以便为认证传递检测测试。

将 sarif 文件放置在 .vcxproj 文件所在的同一目录中，并为其生成 DVL。  如果文件以 *". sarif"* 结尾，则结果文件的确切名称并不重要。 在 WDK 中提供提交 SARIF 结果文件的功能，预览版本20190及更高版本。

有关如何生成 DVL 的说明，请参阅 [创建驱动程序验证日志](../develop/creating-a-driver-verification-log.md)。 有关静态工具徽标 HLK 测试的 DVL 放置位置的指南，请参阅 [运行测试](/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae#running-the-test)。