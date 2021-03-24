---
title: CodeQL 和静态工具徽标测试
description: 在 Windows 驱动程序源代码中使用静态工具和 CodeQL 来发现并修复任何被视为 Must-Fix 的问题
keywords:
- 动态验证工具 WDK
- 静态验证工具 WDK
ms.date: 02/03/2021
ms.localizationpriority: medium
ms.openlocfilehash: bfe98890e0aca02b13fe97f7b4f89f46d96c435e
ms.sourcegitcommit: 01179a569921e3b9a5e2fa56e46164346e581a7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895697"
---
# <a name="codeql-and-the-static-tools-logo-test"></a>CodeQL 和静态工具徽标测试

Microsoft 致力于缓解 Windows 操作系统的攻击面，并确保第三方驱动程序满足强安全块对于实现该目标至关重要。  设置此安全栏的一步是 Microsoft 正在采取的操作是向 [Windows 硬件兼容性计划](/windows-hardware/design/compatibility) 添加新要求 (WHCP) 。  此要求表明所有驱动程序提交必须对驱动程序源代码使用 [CodeQL](https://securitylab.github.com/tools/codeql) 引擎，并修复任何被视为 **"必须修复"** 的冲突。

GitHub 是[CodeQL](https://securitylab.github.com/tools/codeql)，它是用于保护软件的强大静态分析技术。 大范围的高价值安全查询和强大平台的组合使其成为确保第三方驱动程序代码安全的重要工具。

使用 CodeQL 进行 WHCP 测试的目的是在 **[硬件实验室工具包下接受 ()](/windows-hardware/test/hlk/) 最终用户许可协议**。  对于 WHCP 参与者，HLK 的 EULA 会覆盖 GitHub 的 CodeQL 条款和条件。  在自动分析、CI 或 CD 过程中， **可以将 CodeQL 用于** 分析要作为 WHCP 的一部分提交和认证的驱动程序的常规工程过程的一部分。

[静态工具徽标测试](/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae)将强制对驱动程序源代码进行分析并修复任何 **"必须修复"** 冲突。

本主题介绍如何执行以下操作：

- 使用 CodeQL 分析驱动程序源代码，以了解已知的严重影响安全问题。
- 确保静态工具徽标测试可以使用运行 CodeQL 的结果。
- 确定在 WHCP 中必须运行哪些 **"必须修复"** [查询](#must-fix-queries) ，而不会出现证书错误。

## <a name="concepts-for-codeql"></a>CodeQL 的概念

**CodeQL** 是开发人员用来执行安全分析的分析引擎。  **CodeQL 数据库** 是包含以下内容的目录：

- 从驱动程序源代码中提取的可查询数据。
- 用于直接在源代码中显示查询结果的源引用。  **查询** 可以视为 "检查" 或 "规则"。  每个查询都表示一个要搜索的不同安全漏洞。 有关详细信息，请参阅在 CodeQL 文档中 [编写查询](https://codeql.github.com/docs/writing-codeql-queries/codeql-queries/) 。
- 查询结果。
- 在数据库创建、执行查询和其他操作时生成的日志文件。

本主题详细介绍了如何使用 CodeQL 命令行界面 (CLI) 执行分析，重点介绍适用于 Windows 的驱动程序开发人员。  补充文档可在 [CodeQL 入门](https://codeql.github.com/docs/codeql-cli/getting-started-with-the-codeql-cli/)上找到。

我们将使用 [CodeQL 命令行工具 (CLI) ](https://codeql.github.com/docs/codeql-cli/) 从各种编译和解释语言创建 CodeQL 数据库，然后使用特定于驱动程序的 [查询套件](https://codeql.github.com/docs/codeql-cli/creating-codeql-query-suites/)分析该数据库。

## <a name="codeql-windows-setup"></a>CodeQL Windows 安装程序

### <a name="download-install-and-test-codeql"></a>下载、安装并测试 CodeQL

1. 第一个任务是创建一个包含 CodeQL 的目录。  此示例将使用 `C:\codeql-home\`

```command
C:\> mkdir C:\codeql-home
```

2. 导航到 Github [CodeQL 下载页](https://github.com/github/codeql-cli-binaries/releases/)
3. 下载 zip 文件的最新版本。 例如，64位 Windows "codeql-win64.zip"。
4. 将 zip 文件中的 codeql 文件夹解压缩到目录，例如  `C:\codeql-home\codeql\` 。
5. 通过显示帮助确认 CodeQL 命令是否正常工作。

```command
C:\codeql-home\codeql\>codeql --help
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

### <a name="clone-the-repository-to-access-the-driver-specific-queries"></a>克隆存储库以访问特定于驱动程序的查询

1. 导航至 [Microsoft CodeQL GitHub 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)。

2. [克隆](https://github.com/git-guides/git-clone) 存储库以下载包含驱动程序特定查询的所有 CodeQL 查询和 [查询套件](https://codeql.github.com/docs/codeql-cli/creating-codeql-query-suites/) 。

```command
C:\codeql-home\>git clone https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools.git --recursive
```

> [!NOTE]
> 使用 CodeQL 进行 WHCP 测试的目的是在 **[硬件实验室工具包下接受 ()](/windows-hardware/test/hlk/) 最终用户许可协议**。  对于 WHCP 参与者，HLK 的 EULA 会覆盖 GitHub 的 CodeQL 条款和条件。  在自动分析、CI 或 CD 过程中， **可以将 CodeQL 用于** 分析要作为 WHCP 的一部分提交和认证的驱动程序的常规工程过程的一部分。

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

在此示例中，CodeQL 使用 MSBuild 编译器来处理 c + + 代码，以便对其进行分析。


> [!NOTE]
> CodeQL 不需要使用 MSBuild 或 Visual Studio。 有关支持的编译器的列表，请参阅 [支持的 languges 和框架](https://codeql.github.com/docs/codeql-overview/supported-languages-and-frameworks/) 。

### <a name="example"></a>示例

使用用于生成驱动程序源代码的命令行环境（例如 [企业 Windows 驱动程序工具包 (EWDK) ](../develop/using-the-enterprise-wdk.md)）导航到克隆了存储库的 CodeQL 工具文件夹。 如果要使用 Visual Studio 生成驱动程序，则可以将 CodeQL 查询配置为作为后期生成事件运行，如本主题中的 [Visual Studio 后期生成事件](#visual-studio-post-build-event) 中所述。

此示例将处理评估 GitHub 上提供的 kmdfecho 驱动程序示例。

https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf

下面的示例将 kmdf 示例放在目录中 `C:\codeql-home\drivers\kmdf` 。  

运行以下命令，在 *C:\codeql-home\databases\kmdf* 下创建新的 CodeQL 数据库。

```command
C:\codeql-home>C:\codeql-home\codeql\codeql.cmd database create -l=cpp -s=C:\codeql-home\drivers\kmdf -c "msbuild /t:rebuild "C:\codeql-home\drivers\kmdf\kmdfecho.sln" /p:UseSharedCompilation=false" "C:\codeql-home\databases\kmdf" -j 0
```

*"-J 0"* 标志指示使用的线程数与创建数据库的导入步骤中的 CPU 数量相同。

此示例使用此参数来查找和生成驱动程序项目。 Msbuild 命令必须在路径中可用。

```command
msbuild /t:rebuild "C:\codeql-home\drivers\kmdf\kmdfecho.sln"
```

## <a name="summary-of-directory-locations"></a>目录位置摘要

此时，在我们的示例设置中，将显示以下目录。

| 说明            | 位置                           |
|------------------------|------------------------------------|
| Codeql.exe             | C:\codeql-home\codeql\codeql       |
| C + + 规则              | C:\codeql-home\codeql\cpp          |
| 数据库              | C:\codeql-home\databases           |
| 待测试的驱动程序代码 | C:\codeql-home\drivers\kmdf        |
| 查询套件与驱动程序特定的查询 | C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\suites      |

## <a name="perform-analysis"></a>执行分析

此时，设置已完成，下一步是对驱动程序源代码执行实际分析。

CodeQL CLI 工具可以对在上一步中创建的数据库进行分析，还可以运行查询或查询套件。  以 *CSV* 或 *SARIF* 格式报告发现的输出。

出于本示例的目的，假设要在驱动程序源代码上运行的查询套件是在克隆 [Microsoft CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)时包含的 *windows_driver_recommended qls* 套件。

要执行分析的 *"数据库分析"* 命令使用以下语法：

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
C:\codeql-home\codeql>codeql database analyze --help
Usage: codeql database analyze [OPTIONS] <database> [<query|dir|suite>...]
Analyze a database, producing meaningful results in the context of the source code.

Run a query suite (or some individual queries) against a CodeQL database, producing results, styled as alerts or paths,
in SARIF or another interpreted format.

...

```

若要对 kmdf 回送驱动程序的 qls 查询套件进行 *windows_driver_recommended* 评估，并使用 SARIF 格式返回的结果，请使用以下命令。  *Windows_driver_recommended qls* 查询套件是 Microsoft 为驱动程序开发人员认为非常重要的所有查询的超集。  有关详细信息，请参阅下面的 ["查询套件"](#query-suites) 一节。

```command
C:\codeql-home>c:\codeql-home\codeql\codeql.cmd database analyze "C:\codeql-home\databases\kmdf" windows_driver_recommended.qls --format=sarifv2.1.0 --output=C:\codeql-home\databases\kmdfecho1.sarif -j 0
```

应显示类似于以下内容的输出：

```command
Running queries.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Best Practices\Likely Errors\OffsetUseBeforeRangeCheck.ql.
[1/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Best Practices\Likely Errors\OffsetUseBeforeRangeCheck.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Arithmetic\IntMultToLong.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Arithmetic\BadAdditionOverflowCheck.ql.
[2/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Arithmetic\BadAdditionOverflowCheck.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Arithmetic\SignedOverflowCheck.ql.
[3/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Arithmetic\IntMultToLong.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Conversion\CastArrayPointerArithmetic.ql.
[4/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Conversion\CastArrayPointerArithmetic.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Likely Typos\IncorrectNotOperatorUsage.ql.
[5/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Likely Typos\IncorrectNotOperatorUsage.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Memory Management\PointerOverflow.ql.
[6/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Arithmetic\SignedOverflowCheck.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Memory Management\SuspiciousSizeof.ql.
[7/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Memory Management\SuspiciousSizeof.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Memory Management\UninitializedLocal.ql.
[8/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Memory Management\PointerOverflow.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
[9/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Memory Management\UninitializedLocal.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-121\UnterminatedVarargsCall.ql.
[10/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-190\ComparisonWithWiderType.ql.
[11/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-121\UnterminatedVarargsCall.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-253\HResultBooleanConversion.ql.
[12/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-190\ComparisonWithWiderType.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-457\ConditionallyUninitializedVariable.ql.
[13/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-253\HResultBooleanConversion.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-468\IncorrectPointerScaling.ql.
[14/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-468\IncorrectPointerScaling.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-468\IncorrectPointerScalingVoid.ql.
[15/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-468\IncorrectPointerScalingVoid.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-468\SuspiciousAddWithSizeof.ql.
[16/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-468\SuspiciousAddWithSizeof.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-676\PotentiallyDangerousFunction.ql.
[17/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-676\PotentiallyDangerousFunction.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-704\WcharCharConversion.ql.
[18/22] Found in cache: C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-704\WcharCharConversion.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\ProbableUseAfterFree.ql.
[19/22 comp 1m39s] Compiled C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Security\CWE\CWE-457\ConditionallyUninitializedVariable.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\UseAfterFree.ql.
[20/22 comp 2m24s] Compiled C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\ProbableUseAfterFree.ql.
Compiling query plan for C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\queries\Windows\wdk\wdk-deprecated-api.ql.
[21/22 comp 1m1s] Compiled C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\UseAfterFree.ql.
[22/22 comp 9.6s] Compiled C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\windows-drivers\queries\Windows\wdk\wdk-deprecated-api.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Arithmetic\BadAdditionOverflowCheck.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Memory Management\PointerOverflow.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Memory Management\SuspiciousSizeof.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Arithmetic\SignedOverflowCheck.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Likely Typos\IncorrectNotOperatorUsage.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Conversion\CastArrayPointerArithmetic.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Arithmetic\IntMultToLong.ql.
Starting evaluation of codeql-cpp\Best Practices\Likely Errors\OffsetUseBeforeRangeCheck.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Memory Management\UninitializedLocal.ql.
Starting evaluation of codeql-cpp\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-121\UnterminatedVarargsCall.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-190\ComparisonWithWiderType.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-253\HResultBooleanConversion.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-468\IncorrectPointerScaling.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-468\IncorrectPointerScalingVoid.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-468\SuspiciousAddWithSizeof.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-676\PotentiallyDangerousFunction.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-704\WcharCharConversion.ql.
Starting evaluation of codeql-cpp\Security\CWE\CWE-457\ConditionallyUninitializedVariable.ql.
Starting evaluation of windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\ProbableUseAfterFree.ql.
Starting evaluation of windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\UseAfterFree.ql.
Starting evaluation of windows-drivers\queries\Windows\wdk\wdk-deprecated-api.ql.
[1/22 eval 16.1s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-676\PotentiallyDangerousFunction.bqrs.
[2/22 eval 16.3s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-704\WcharCharConversion.bqrs.
[3/22 eval 17.5s] Evaluation done; writing results to codeql-cpp\Best Practices\Likely Errors\OffsetUseBeforeRangeCheck.bqrs.
[4/22 eval 17.6s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Memory Management\SuspiciousSizeof.bqrs.
[5/22 eval 16.5s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-468\SuspiciousAddWithSizeof.bqrs.
[6/22 eval 17.6s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Arithmetic\BadAdditionOverflowCheck.bqrs.
[7/22 eval 17.7s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Likely Typos\IncorrectNotOperatorUsage.bqrs.
[8/22 eval 16.9s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-253\HResultBooleanConversion.bqrs.
[9/22 eval 18.5s] Evaluation done; writing results to windows-drivers\queries\Windows\wdk\wdk-deprecated-api.bqrs.
[10/22 eval 19.4s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Underspecified Functions\TooFewArguments.bqrs.
[11/22 eval 19.2s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-121\UnterminatedVarargsCall.bqrs.
[12/22 eval 23.4s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-468\IncorrectPointerScaling.bqrs.
[13/22 eval 23.2s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-468\IncorrectPointerScalingVoid.bqrs.
[14/22 eval 26.3s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Memory Management\UninitializedLocal.bqrs.
[15/22 eval 31.7s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Conversion\CastArrayPointerArithmetic.bqrs.
[16/22 eval 32s] Evaluation done; writing results to windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\ProbableUseAfterFree.bqrs.
[17/22 eval 33.5s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Arithmetic\IntMultToLong.bqrs.
[18/22 eval 33.5s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-190\ComparisonWithWiderType.bqrs.
[19/22 eval 33.8s] Evaluation done; writing results to codeql-cpp\Security\CWE\CWE-457\ConditionallyUninitializedVariable.bqrs.
[20/22 eval 36.5s] Evaluation done; writing results to windows-drivers\queries\Likely Bugs\Memory Management\UseAfterFree\UseAfterFree.bqrs.
[21/22 eval 38.9s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Memory Management\PointerOverflow.bqrs.
[22/22 eval 46.1s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Arithmetic\SignedOverflowCheck.bqrs.
Shutting down query evaluator.
Interpreting results.
```

您可以使用 *"– timeout = [秒]"* 标志为整个操作指定超时。  这可用于分析查询，而不受单个长时间运行的查询的限制。  [数据库分析](https://codeql.github.com/docs/codeql-cli/analyzing-databases-with-the-codeql-cli/)中介绍了更多用于调整分析优化的选项。 

## <a name="query-suites"></a>查询套件

作为 [Microsoft CodeQL GitHub 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)的一部分，microsoft 提供了两个查询套件来简化端到端驱动程序开发人员工作流。  *Windows_driver_recommended qls* 查询套件包含 Microsoft 认为对驱动程序开发人员非常宝贵的 [所有查询](#queries)的超集。  

Qls 查询套件包含当前被视为用于 WHCP 认证的 **"必须修复"** 的 [查询](#must-fix-queries)。 *windows_driver_mustfix* 这两个查询套件会定期更新，因为 Microsoft 最终会获得可用查询列表和 WHCP 认证所需的 "必须修复" 查询列表。  因此，使用 ["git pull"](https://www.git-scm.com/docs/git-pull) 命令定期同步存储库至关重要。

## <a name="troubleshooting"></a>故障排除

对于 [数据库版本](https://codeql.github.com/docs/codeql-cli/manual/version/) 不匹配问题，下列工具可能有所帮助。

使用 "codeql 版本" 命令显示 codeql exe 的版本。

```command
C:\codeql-home\codeql\>codeql version
CodeQL command-line toolchain release 2.4.0.
Copyright (C) 2019-2020 GitHub, Inc.
Unpacked in: C:\codeql-home\codeql\
   Analysis results depend critically on separately distributed query and
   extractor modules. To list modules that are visible to the toolchain,
   use 'codeql resolve qlpacks' and 'codeql resolve languages'.
```

数据库升级命令将更新数据库。 请注意，这是一个单向升级，不可逆。 有关详细信息，请参阅 [数据库升级](https://codeql.github.com/docs/codeql-cli/upgrading-codeql-databases/)。

## <a name="queries"></a>查询

此页将会更新，以指示对于 WHCP 认证，哪些查询已被正式视为 **"必须修复"** 。

Microsoft 建议在 *所有* 驱动程序源代码上运行的查询包括：

| ID                       | 位置   | [常见漏洞枚举](https://cwe.mitre.org/)   |
| ------------------------ | ---------- | ----------------------------- |
| [cpp/参数太少](https://codeql.github.com/codeql-query-help/cpp/cpp-too-few-arguments/)   | *cpp/q/src/可能的 Bug/Underspecified 函数/TooFewArguments. q* | 不适用 |
| [cpp/错误添加-溢出-检查](https://codeql.github.com/codeql-query-help/cpp/cpp-bad-addition-overflow-check/)   | *cpp/q/src/可能的 Bug/算数/BadAdditionOverflowCheck. q* | [CWE-190](https://cwe.mitre.org/data/definitions/190.html)， [CWE-192](https://cwe.mitre.org/data/definitions/192.html) |
| [cpp/指针溢出-检查](https://codeql.github.com/codeql-query-help/cpp/cpp-pointer-overflow-check/)   | *cpp/q/src/可能的 Bug/内存管理/PointerOverflow. q* | 不适用 |
| [cpp/hresult-布尔转换](https://codeql.github.com/codeql-query-help/cpp/cpp-hresult-boolean-conversion/)   | *cpp/q/src/Security/CWE/CWE-253/HResultBooleanConversion. q* | [CWE-253](https://cwe.mitre.org/data/definitions/253.html) |
| [cpp/错误的字符串类型转换](https://codeql.github.com/codeql-query-help/cpp/cpp-incorrect-string-type-conversion/)   | *cpp/q/src/Security/CWE/CWE-704/WcharCharConversion. q* | [CWE-704](https://cwe.mitre.org/data/definitions/704.html) |
| [cpp/整数-强制转换为 long](https://codeql.github.com/codeql-query-help/cpp/cpp-integer-multiplication-cast-to-long/)   | *cpp/q/src/可能的 Bug/算数/IntMultToLong. q* | [CWE-190](https://cwe.mitre.org/data/definitions/190.html)、 [CWE-192](https://cwe.mitre.org/data/definitions/192.html)、 [CWE-197](https://cwe.mitre.org/data/definitions/197.html)、 [CWE-681](https://cwe.mitre.org/data/definitions/681.html) |
| [cpp/有符号溢出-检查](https://codeql.github.com/codeql-query-help/cpp/cpp-signed-overflow-check/)   | *cpp/q/src/可能的 Bug/算数/SignedOverflowCheck. q* | 不适用 | 
| [cpp/向上转换-数组指针算法](https://codeql.github.com/codeql-query-help/cpp/cpp-upcast-array-pointer-arithmetic/)   | *cpp/q/src/可能的 Bug/转换/CastArrayPointerArithmetic。 q* | [CWE-119](https://cwe.mitre.org/data/definitions/119.html)， [CWE-843](https://cwe.mitre.org/data/definitions/843.html) |
| [cpp/比较-具有更大的类型](https://codeql.github.com/codeql-query-help/cpp/cpp-comparison-with-wider-type/)   | *cpp/q/src/Security/CWE/CWE-190/ComparisonWithWiderType. q* | [CWE-190](https://cwe.mitre.org/data/definitions/190.html)、 [CWE-197](https://cwe.mitre.org/data/definitions/197.html)、 [CWE-835](https://cwe.mitre.org/data/definitions/835.html) |
| [cpp/可疑-添加-sizeof](https://codeql.github.com/codeql-query-help/cpp/cpp-suspicious-add-sizeof/)   | *cpp/q/src/Security/CWE/CWE-468/SuspiciousAddWithSizeof q* | [CWE-468](https://cwe.mitre.org/data/definitions/468.html) |
| [cpp/可能危险的函数](https://codeql.github.com/codeql-query-help/cpp/cpp-potentially-dangerous-function/)   | *cpp/q/src/Security/CWE/CWE-676/PotentiallyDangerousFunction q* | [CWE-676](https://codeql.github.com/codeql-query-help/cpp/cpp-potentially-dangerous-function/) 
| [cpp/不正确-用法](https://codeql.github.com/codeql-standard-libraries/cpp/Likely%20Bugs/Likely%20Typos/IncorrectNotOperatorUsage.ql/module.IncorrectNotOperatorUsage.html)   | *cpp/q/src/可能的 Bug/错误录入/IncorrectNotOperatorUsage。 q* | [CWE-480](https://cwe.mitre.org/data/definitions/480.html) |
| [cpp/offset-使用前-范围-检查](https://github.com/github/codeql/blob/main/cpp/ql/src/Best%20Practices/Likely%20Errors/OffsetUseBeforeRangeCheck.qhelp)  | *cpp/q/src/最佳方案/可能的错误/OffsetUseBeforeRangeCheck. q*   | 不适用 |
| [cpp/可疑-添加-sizeof](https://codeql.github.com/codeql-query-help/cpp/cpp-suspicious-add-sizeof/)   | *cpp/q/src/可能的 Bug/内存管理/SuspiciousSizeof. q* | [CWE-468](https://codeql.github.com/codeql-query-help/cpp/cpp-suspicious-add-sizeof/) |
| [cpp/未初始化-本地](https://codeql.github.com/codeql-standard-libraries/cpp/Likely%20Bugs/Memory%20Management/UninitializedLocal.ql/module.UninitializedLocal.html)   | *cpp/q/src/可能的 Bug/内存管理/UninitializedLocal. q* | [CWE-457](https://cwe.mitre.org/data/definitions/457.html)， [CWE-665](https://cwe.mitre.org/data/definitions/665.html) |
| [cpp/未终止-可变参数-调用](https://codeql.github.com/codeql-standard-libraries/cpp/Security/CWE/CWE-121/UnterminatedVarargsCall.ql/module.UnterminatedVarargsCall.html)   | *cpp/q/src/Security/CWE/CWE-121/UnterminatedVarargsCall. q* | [CWE-121](https://cwe.mitre.org/data/definitions/121.html) |
| [cpp/可疑指针缩放](https://github.com/github/codeql/blob/main/cpp/ql/src/Security/CWE/CWE-468/IncorrectPointerScalingChar.qhelp)   | *cpp/q/src/Security/CWE/CWE-468/IncorrectPointerScaling q* | [CWE-468](https://cwe.mitre.org/data/definitions/468.html) |
| [cpp/可疑-指针缩放-void](https://github.com/github/codeql/blob/main/cpp/ql/src/Security/CWE/CWE-468/IncorrectPointerScalingVoid.qhelp)   | *cpp/q/src/Security/CWE/CWE-468/IncorrectPointerScalingVoid q* | [CWE-468](https://cwe.mitre.org/data/definitions/468.html) |
| [cpp/有条件-未初始化-变量](https://codeql.github.com/codeql-standard-libraries/cpp/Security/CWE/CWE-457/ConditionallyUninitializedVariable.ql/module.ConditionallyUninitializedVariable.html)   | *cpp/q/src/Security/CWE/CWE-457/ConditionallyUninitializedVariable。* | [CWE-457](https://cwe.mitre.org/data/definitions/457.html) |
| [cpp/使用-免费](./codeql-windows-driver-useafterfree.md)   | *Windows 驱动程序-开发人员补充-工具/codeql/windows-驱动程序/查询/可能的 Bug/内存管理/UseAfterFree \ UseAfterFree q* | 不适用 |
| [cpp/windows/wdk/弃用的 api](./codeql-windows-driver-wdkdeprecatedapi.md)   | *Windows 驱动程序-开发人员补充-工具/codeql/windows-驱动程序/查询/Windows/wdk/wdk-q* | 不适用 |

这些查询是 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中的 *windows_driver_recommended qls* 查询套件的一部分。  "常见漏洞枚举" (CWE) 列指定给定查询搜索的安全问题类型。  有关 CWE 的详细信息，请参阅 [CWE 上的 Mitre 页面](https://cwe.mitre.org/) 。 

### <a name="must-fix-queries"></a>Must-Fix 查询

下面的查询子集当前被视为 WHCP 认证的 **"必须修复"** 。  **此列表可能会更改**。  2021年4月1日，最终列表将发布到此页。  

| ID            | 位置 | [常见漏洞枚举](https://cwe.mitre.org/)   |
| ------------------------ | ---------- | ----------------------------- |
| [cpp/参数太少](https://codeql.github.com/codeql-query-help/cpp/cpp-too-few-arguments/)   | *cpp/q/src/可能的 Bug/Underspecified 函数/TooFewArguments. q* | 不适用 |
| [cpp/错误添加-溢出-检查](https://codeql.github.com/codeql-query-help/cpp/cpp-bad-addition-overflow-check/)   | *cpp/q/src/可能的 Bug/算数/BadAdditionOverflowCheck. q* | [CWE-190](https://cwe.mitre.org/data/definitions/190.html)， [CWE-192](https://cwe.mitre.org/data/definitions/192.html) |
| [cpp/指针溢出-检查](https://codeql.github.com/codeql-query-help/cpp/cpp-pointer-overflow-check/)   | *cpp/q/src/可能的 Bug/内存管理/PointerOverflow. q*| 不适用 |
| [cpp/hresult-布尔转换](https://codeql.github.com/codeql-query-help/cpp/cpp-hresult-boolean-conversion/)   | *cpp/q/src/Security/CWE/CWE-253/HResultBooleanConversion. q* | [CWE-253](https://cwe.mitre.org/data/definitions/253.html) |
| [cpp/错误的字符串类型转换](https://codeql.github.com/codeql-query-help/cpp/cpp-incorrect-string-type-conversion/)   | *cpp/q/src/Security/CWE/CWE-704/WcharCharConversion. q* | [CWE-704](https://cwe.mitre.org/data/definitions/704.html) |
| [cpp/有条件-未初始化-变量](https://codeql.github.com/codeql-standard-libraries/cpp/Security/CWE/CWE-457/ConditionallyUninitializedVariable.ql/module.ConditionallyUninitializedVariable.html)   | *cpp/q/src/Security/CWE/CWE-457/ConditionallyUninitializedVariable。* | [CWE-457](https://cwe.mitre.org/data/definitions/457.html) |
| [cpp/比较-具有更大的类型](https://codeql.github.com/codeql-query-help/cpp/cpp-comparison-with-wider-type/)   | *cpp/q/src/Security/CWE/CWE-190/ComparisonWithWiderType. q*  | [CWE-190](https://cwe.mitre.org/data/definitions/190.html)、 [CWE-197](https://cwe.mitre.org/data/definitions/197.html)、 [CWE-835](https://cwe.mitre.org/data/definitions/835.html) |
| [cpp/未初始化-本地](https://codeql.github.com/codeql-standard-libraries/cpp/Likely%20Bugs/Memory%20Management/UninitializedLocal.ql/module.UninitializedLocal.html)   | *cpp/q/src/可能的 Bug/内存管理/UninitializedLocal. q* | [CWE-457](https://cwe.mitre.org/data/definitions/457.html)， [CWE-665](https://cwe.mitre.org/data/definitions/665.html) |
| [cpp/windows/wdk/弃用的 api](./codeql-windows-driver-wdkdeprecatedapi.md)   | *Windows 驱动程序-开发人员补充-工具/codeql/windows-驱动程序/查询/Windows/wdk/wdk-q* | 不适用 |

这些查询是 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中的 *windows_driver_mustfix qls* 查询套件的一部分。

## <a name="view-analysis"></a>查看分析

在上一部分中运行分析命令的结果可以 [SARIF](https://codeql.github.com/docs/codeql-overview/codeql-glossary/#sarif-file) 文件格式查看。  有关 SARIF 输出的详细信息可在 [SARIF 输出](https://codeql.github.com/docs/codeql-cli/sarif-output/)中找到。 有关 SARIF 标准的信息，请参阅 [OASIS 静态分析结果交换格式 (SARIF) ](https://github.com/oasis-tcs/sarif-spec)。

SARIF 文件包含已运行的每个查询的 " **结果** " 部分，其中包含有关已完成分析的详细信息。  例如，如果查询发现一个漏洞，则 SARIF 文件将包含该漏洞的详细信息以及发现缺陷的位置的详细信息。 如果未找到任何漏洞，则结果部分将为空。

```xml
    "results" : [ ],
```

若要查看结果，请安装 [适用于 Visual Studio 的 MICROSOFT SARIF 查看器](https://marketplace.visualstudio.com/items?itemName=WDGIS.MicrosoftSarifViewer) 并按照该页上的说明进行操作。  或者，你可以 [为 Visual Studio Code 安装 SARIF 扩展](https://marketplace.visualstudio.com/items?itemName=MS-SarifVSCode.sarif-viewer)。

> [!NOTE]
> 请务必注意，对于使用静态工具徽标测试进行验证的驱动程序， **应忽略** 查询的 "错误"、"警告" 或 "问题" 的分类。  如果驱动程序在标记为 ["必须修复"](#must-fix-queries)的查询中具有缺陷，则 **不会传递静态工具徽标测试** ，而与原始查询文件中的查询分类无关 (ie。"警告" ) 。 
## <a name="driver-verification-log-dvl-consumption-of-sarif-output"></a>SARIF 输出的驱动程序验证日志 (DVL) 消耗

Microsoft 将强制要求在静态工具徽标测试中运行 CodeQL 查询。  静态工具徽标测试使用 [驱动程序验证日志 (DVL) ](../develop/creating-a-driver-verification-log.md) 从在驱动程序源代码上运行的不同静态分析中收集结果。  然后，将此 DVL 分析为在 HLK 测试中使用的静态工具徽标测试的一部分。

CodeQL 结果遵循相同的模型，该模型使用 DVL 来表明要认证的驱动程序运行了相应的 CodeQL 查询，以便为认证传递检测测试。

将 sarif 文件放置在 .vcxproj 文件所在的同一目录中，并为其生成 DVL。  如果文件以 *". sarif"* 结尾，则结果文件的确切名称并不重要。 在 WDK 中提供提交 SARIF 结果文件的功能，预览版本20190及更高版本。

有关如何生成 DVL 的说明，请参阅 [创建驱动程序验证日志](../develop/creating-a-driver-verification-log.md)。 有关静态工具徽标 HLK 测试的 DVL 放置位置的指南，请参阅 [运行测试](/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae#running-the-test)。

## <a name="visual-studio-post-build-event"></a>Visual Studio 生成后事件

如果使用 Visual Studio 构建驱动程序，则可以将 CodeQL 查询配置为作为后期生成事件运行。

在此示例中，将在目标位置中创建一个小的批处理文件，并将其称为 "后期生成事件"。 有关 Visual Studio c + + 生成事件的详细信息，请参阅 [指定生成事件](/cpp/build/specifying-build-events)。

1. 创建一个小型批处理文件，该文件重新创建 CodeQL 数据库，然后使用最新的数据库运行所需的查询。  在此示例中，批处理文件将命名为 `RunCodeQLRebuildQuery.bat` 。 修改示例批处理文件中显示的路径，以匹配目录位置。

```command
ECHO ">>> Running CodeQL Security Rule V 1.0 <<<"
ECHO ">>> Removing previously created rules database <<<"
rmdir /s/q C:\codeql-home\databases\kmdf
CALL C:\codeql-home\codeql\codeql\codeql.cmd database create -l=cpp -s="C:\codeql-home\drivers\kmdf" -c "msbuild /p:Configuration=Release /p:Platform=x64 C:\codeql-home\drivers\kmdf\kmdfecho.sln /t:rebuild /p:PostBuildEventUseInBuild=false " "C:\codeql-home\databases\kmdf" -j 0
CALL C:\codeql-home\codeql\codeql\codeql database analyze "C:\codeql-home\databases\kmdf" "C:\codeql-home\Windows-Driver-Developer-Supplemental-Tools\codeql\codeql-queries\cpp\ql\src\Likely Bugs\Underspecified Functions" --format=sarifv2.1.0 --output=C:\codeql-home\databases\kmdf.sarif -j 0 --rerun
ECHO ">>> Loading SARIF Results in Visual Studio <<<"
CALL devenv /Edit C:\codeql-home\databases\kmdf.sarif
SET ERRORLEVEL = 0
```

2. 在批处理文件中使用 [devenv.exe/Edit](/visualstudio/ide/reference/edit-devenv-exe) 选项，以在 Visual Studio 的现有实例中打开 SARIF 结果文件。 若要查看 SARIF 结果，请安装 [适用于 Visual Studio 的 MICROSOFT SARIF 查看器](https://marketplace.visualstudio.com/items?itemName=WDGIS.MicrosoftSarifViewer)。 有关详细信息，请参阅该页上的说明。

3. 在驱动程序项目中，导航到 "项目属性"。 在 "  **配置** " 下拉配置中，选择要用 CodeQL 检查的生成配置。 例如，" *发布* " 配置。 因为创建 CodeQL 数据库并运行查询需要几分钟时间，所以你可能会决定不在项目的调试配置上运行 CodeQL。

4. 在驱动程序项目属性中选择 " **生成事件** " 和 "生成 **后事件** "。

5. 提供批处理文件的路径和后期生成事件的说明。

![显示配置为命令行选项的批处理文件的 Visual Studio 后期生成事件配置](images/codeql-visual-studio-post-build-event.png)

6. 当项目生成时，在生成输出结束时，将显示运行批处理文件的结果。

```command
...

1>Starting evaluation of codeql-cpp\Likely Bugs\Underspecified Functions\MistypedFunctionArguments.ql.
1>Starting evaluation of codeql-cpp\Likely Bugs\Underspecified Functions\TooManyArguments.ql.
1>Starting evaluation of codeql-cpp\Likely Bugs\Underspecified Functions\TooFewArguments.ql.
1>Starting evaluation of codeql-cpp\Likely Bugs\Underspecified Functions\ImplicitFunctionDeclaration.ql.
1>[1/4 eval 4.4s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Underspecified Functions\TooManyArguments.bqrs.
1>[2/4 eval 4.4s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Underspecified Functions\TooFewArguments.bqrs.
1>[3/4 eval 4.5s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Underspecified Functions\ImplicitFunctionDeclaration.bqrs.
1>[4/4 eval 5.2s] Evaluation done; writing results to codeql-cpp\Likely Bugs\Underspecified Functions\MistypedFunctionArguments.bqrs.
1>Shutting down query evaluator.
1>Interpreting results.
1>">>> Loading SARIF Results in Visual Studio <<<"
```

7. 查看 SARIF 文件的结果，并解决任何已确定的问题。 有关详细信息，请参阅本主题前面的 [查看分析](#view-analysis) 。

## <a name="frequently-asked-questions-faqs"></a>常见问题 (常见问题解答) 

#### <a name="when-will-this-be-required-for-device-certification"></a>何时需要此设备认证？

有关此要求生效的详细信息，请参阅最新的 WHCP 要求。

#### <a name="what-is-the-motivation-behind-requiring-codeql-be-run-on-driver-source-code"></a>要求 CodeQL 在驱动程序源代码上运行的动机是什么？

需要在驱动程序源代码上运行 CodeQL 的动机可以通过两个主要原因进行汇总：

1. Windows 的安全性非常重要。  要求在驱动程序源代码上运行 CodeQL 是一步，是确保 Microsoft 认证的组件是安全的。
2. [Microsoft 在 microsoft 使用](https://msrc-blog.microsoft.com/2018/08/16/vulnerability-hunting-with-semmle-ql-part-1/)CodeQL 来查找安全缺陷，而 CodeQL 查询则由 microsoft 的安全工程师积极开发。  Microsoft 致力于确保其硬件生态系统受益于 Microsoft 使用的同一优质工具。

#### <a name="which-license-governs-the-usage-of-codeql-for-driver-developers"></a>哪个许可证控制驱动程序开发人员对 CodeQL 的使用？

使用 CodeQL 进行 WHCP 测试的目的是在 **[硬件实验室工具包下接受 ()](/windows-hardware/test/hlk/) 最终用户许可协议**。  对于 WHCP 参与者，HLK 的 EULA 会覆盖 GitHub 的 CodeQL 条款和条件。  在自动分析、CI 或 CD 过程中， **可以将 CodeQL 用于** 分析要作为 WHCP 的一部分提交和认证的驱动程序的常规工程过程的一部分。

#### <a name="do-i-need-to-use-visual-studio-or-msbuild-to-run-codeql"></a>是否需要使用 Visual Studio 或 msbuild 来运行 CodeQL？

CodeQL 不 **需要使用 MSBuild 或 Visual Studio**。 有关支持的编译器的列表，请参阅 [支持的 languges 和框架](https://codeql.github.com/docs/codeql-overview/supported-languages-and-frameworks/) 。

#### <a name="how-does-the-hlk-verify-that-my-driver-was-scanned-by-codeql"></a>HLK 如何验证我的驱动程序是否已由 CodeQL 扫描？

"HLK 中的静态工具徽标测试" 是强制实施此要求的测试。  有关如何传递静态工具徽标测试的详细信息，请参阅其 [MS 文档页](/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae)。

#### <a name="can-i-generate-a-dvl-on-visual-studio-solutions"></a>能否在 Visual Studio 解决方案中生成 DVL？ 

不需要，DVL 生成必须在项目级别运行，并且不能在 [Visual Studio 解决方案](/visualstudio/get-started/tutorial-projects-solutions#:~:text=A%20solution%20is%20simply%20a,projects%20that%20the%20solution%20contains.)中运行。

#### <a name="are-all-defects-reported-by-codeql-true-defects"></a>是否所有缺陷都是由 CodeQL 报告的吗？

每个 CodeQL 查询都有不同的精度级别。  目标是将误报降到最低，但会按定义发生。  已手动选取 "必须修复" 查询集，因为经过广泛的测试后，就会发现将近0个误报。  如果从 "必须修复" 查询集的查询中看到误报，请立即 **发送电子邮件 stlogohelp@microsoft.com** 。

#### <a name="does-a-querys-classification-of-either-warning-or-error-matter-for-the-purposes-of-the-static-tools-logo-test"></a>查询对静态工具徽标测试的 "警告" 或 "错误" 的分类是否重要？

请务必注意，对于使用静态工具徽标测试进行验证的驱动程序， **应忽略** 查询的 "错误"、"警告" 或 "问题" 的分类。  如果驱动程序在标记为 ["必须修复"](#must-fix-queries)的查询中具有缺陷，则 **不会传递静态工具徽标测试** ，而与原始查询文件中的查询分类无关 (ie。"警告" ) 。 

#### <a name="i-have-comments-or-questions-around-how-to-use-codeql-on-my-driver-where-do-i-send-feedback"></a>我有关于如何在我的驱动程序上使用 CodeQL 的评论或疑问，我会在何处发送反馈？

将所有反馈和问题发送到 [stlogohelp@microsoft.com](mailto:stlogohelp@microsoft.com) 。