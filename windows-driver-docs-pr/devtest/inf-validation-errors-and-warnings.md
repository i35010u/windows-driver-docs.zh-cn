---
title: INF 验证错误和警告
description: 驱动程序安装错误和警告可以显示作为 Microsoft Visual Studio 将执行自动 INF 验证结果。
ms.assetid: E021D8F8-BFDA-4F71-B8EA-0997096761FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6caa307ecdfe6a720f8f1050c89193a9a6e72040
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360785"
---
# <a name="inf-validation-errors-and-warnings"></a>INF 验证错误和警告

本主题介绍驱动程序安装错误和警告可以显示作为自动 INF 验证结果，Microsoft Visual Studio 执行或运行时[InfVerif](infverif.md)工具。

从 Visual Studio 2015 with WDK 10 在生成您的驱动程序时，以下的 INF 文件错误可以出现在错误列表窗格。 如果从命令行运行 InfVerif.exe，工具会在命令提示符下或结果的 HTML 版本中显示这些错误。

## <a name="error-guidance"></a>错误的指南

InfVerif 如下所示的常规规则，较低的错误号、 更严重问题。
大多数的错误代码可以是一条警告或错误具体取决于提供给 InfVerif 的参数。

### <a name="handling-errors"></a>处理错误

若要通过硬件开发人员中心仪表板上的驱动程序测试，必须修复所有错误。 错误与以下条件：

- INF 分析器是无法成功解释您 INF
- INF 分析器是能够解释 INF 只能通过进行默认值假设 （不明确的语法）
- InfVerif 的参数指示规则集，应该应用于 INF （如通用）

而无需提交您的驱动程序开发人员中心上之前修复警告，建议花时间去理解报告的问题。 如果不了解给定的警告，你 INF 可能不始终按预期工作。

警告通常与相关：

- 它可能不正确，但具有有效情况下，在相应的语法
- 为给定的 InfVerif 参数有效，但在其他模式下，例如通用错误的语法

如果，则将显示与通用设置相关的问题的错误为：

- 在 Visual Studio 中，你构建您的驱动程序与目标平台设置为**通用**或**移动**。
- 从命令行运行 InfVerif.exe，并指定 /u 标志。

与通用设置相关的问题显示为警告，如果：

- 在 Visual Studio 中，你构建您的驱动程序与目标平台设置为**桌面**。
- 从命令行运行 InfVerif.exe 和未指定 /u 标志。

## <a name="error-codes"></a>错误代码

错误代码分为以下分类：

- [INF 文件 (1100年 1299) 中的语法](#syntax-in-the-inf-file-1100-1299)
- [通用 INF (1300年 1319)](#universal-inf-1300-1319)
- [安装 (2000年-2999)](#installation-2000-2999)

并非所有错误代码下面都列出了，因为不证自明的许多含义。 1000 1099年范围内的错误被视为不证自明的因为它们是基本语法错误。

## <a name="syntax-in-the-inf-file-1100-1299"></a>INF 文件 (1100年 1299) 中的语法

虽然 InfVerif 失败意味着驱动程序提交失败，仍然可能会成功安装驱动程序。
这是因为在安装驱动程序，如果错误是 INF 文件中存在，Windows 还会尝试设置的默认值。
Windows 不会由于此范围内的错误的驱动程序安装失败，但在此范围内的错误指示行为可能会更改具体取决于 OS 版本或 SKU。
在其中该驱动程序安装成功的情况下，这些错误指示存在*是*情况下，该驱动程序可能无法正确安装。

<table>
<thead>
<tr>
<th>错误代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1100:DriverStore Copyfile 名称不匹配</strong></td>
<td>复制或从其原始的驱动程序存储区名称和位置重命名为不同的名称和位置中的驱动程序文件时，将出现此错误。  例如：
<pre>
[SourceDisksFiles]
DriverFile.sys=1,x64  

[DestinationDirs]
CopyFileSection=13,SubDirectory  
  
[CopyFileSection]
DriverFile.sys
</pre>
驱动程序存储区维护原始的驱动程序包目录结构。  在上面的代码中，是 DriverFile.sys 的原始位置<i>INF 位置</i>\x64，但 CopyFiles 指令将其放入<i>INF 位置</i>\SubDirectory。  将该文件已重命名为副本的一部分显示的相同错误。</td>
</tr>
<tr>
<td><strong>1203:找不到的部分</strong></td>
<td>例如，以下 INF 语法会导致错误 1203年:
<pre>
[MyInstallSection]
CopyFiles=driverFile.sys
</pre>
会报告此错误，因为<strong>CopyFiles</strong>指令需要一个部分名称 （用于指定要复制的文件列表）。 但是， <strong>CopyFiles</strong>指令可以指定文件的名称。 若要区分节名称和文件名称，前面加上文件名包含 @ 令牌如下所示：
<pre>
[MyInstallSection]
CopyFiles=@driverFile.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1204:提供程序不能为 Microsoft</strong></td>
<td>[Version] 部分中的提供程序字段不能指定 Microsoft。
<pre>
[Version]
Signature="$Windows NT$"
Class=Sample
ClassGuid={78A1C341-4539-11d3-B88D-00C04FAD5171}
Provider="Microsoft"
</pre>
</td>
</tr>
<tr>
<td><strong>1205:从 [Directive1] 引用部分 [Driver_files] 和 [Directive2] 指令</td>
<td>每当两个不同的指令指向同一部分时，会生成此警告。
  <p>请注意，尽管在大多数情况下这一点，实际上，出现错误，在某些情况下 1205年报告即使条件正是目的也是如此。</td>
</tr>
<tr>
<td><strong>1212:不能有两个 [DefaultInstall] 和 [制造商]</strong></td>
<td>单个 INF 不能包含这两个 [DefaultInstall] 和 [制造商]。  使用同时创作 Inf 应删除其中一个的两个部分。
</td>
</tr>
<tr>
<td><strong>1220:不能直接引用定义中包含的 INF 部分</strong></td>
<td>如果您的 INF 文件引用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547344">DDInstall</a>部分中包含的 INF，必须使用<strong>需要</strong>指令。 引用一个部分中包含的 INF 的任何其他指令会导致错误 1220年。
<p>在此示例中，A.INF 的安装部分引用中 B.INF 等效安装部分。</p>
<p>A.INF 包含：</p>
<div class="code">
<pre>
A.INF
[InstallSectionA]
Include = B.INF
Needs = InstallSectionB
AddReg = AddRegB ; WARNING 1220

[InstallSectionA.Services]
Include = B.INF
Needs = InstallSectionB.Services
</pre>
<p>B.INF 包含：</p>
<pre>
B.INF
[InstallSectionB]
AddReg = AddRegB
[InstallSectionB.Services]
...

[AddRegB]
...
</pre>
</div>
<p><strong>需要</strong>指令必须引用来处理在安装部分中的等效安装部分。 例如，[InstallSectionA.Services] 中的需求指令应指向。另一个安装部分的服务。 <strong>需要</strong>指令还可用于添加另一个 DDInstall 部分中的相同 INF 此行为。 使用<strong>需要</strong>指令在其他类型的部分可能会导致意外行为。</p></td>
</tr>
<tr>
<td><strong>1221:不能修改服务注册密钥，必须使用 HKR</strong></td>
<td>此错误表示 INF 文件，例如引用在服务注册表项的位置<strong>HKLM\SYSTEM\CurrentControlSet\Services&lt;em&gt;服务名称</em></strong>。 当访问服务密钥，则应改用相对的根 (<strong>HKR</strong>) 能够在设备或驱动程序实例相关联的注册表值。
<p>当你使用<strong>HKR</strong>，注册表值将不会显示之前安装该设备。</p></td>
</tr>
<tr>
<td><strong>1230:缺少文件 [SourceDisksFiles] 部分下的 xxxx。</strong></td>
<td>这表示为驱动程序包的一部分指定了文件，但在 [SourceDisksFiles] 部分中未指定相对于 INF 文件的源位置。
<pre>
[SourceDisksFiles]
filename=disk id
</pre>
请注意，如果指定的 [SourceDisksFiles] 修饰体系结构的版本，经常发生此错误 (如 [SourceDisksFiles.amd64]，但并非所有体系结构支持的 INF 具有 [SourceDisksFiles] 部分。</td>
</tr>
<tr>
<td><strong>1233:缺少指令所需的签名</strong></td>
<td>在 [Version] 部分中，必须指定一个 CatalogFile 指令 （和关联的目录文件） 以接收签名驱动程序包上。
<pre>
CatalogFile=wudf.cat
</pre>
</td>
</tr>
<tr>
<td><strong>1235:字符串 [Strings] 中未定义的标记</strong></td>
<td>指定的字符串标记有 [Strings] 部分中没有定义。 例如，INF 文件指定<em>%reg_dword%</em>中<em>添加注册表部分</em>指定的<a href="https://msdn.microsoft.com/library/windows/hardware/ff546320"> <strong>AddReg</strong> </a>指令，但没有没有相应的 REG_DWORD = 中的 0x00010001 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547485">[Strings]</a>部分。
<p>如果您的 INF 文件指定一个包含环境变量的注册表值，通常会出现此错误。 例如：</p>
<pre>
[MyAddReg]
HKR,,DllPath,%SystemRoot%\System32\myDll.sys
</pre>
此行会导致 INF 分析器尝试找到令牌"SystemRoot"从 [Strings] 部分中，而不是在注册表中存储文本"%systemroot%"的预期的行为。  若要使用的文本值 %systemroot%而不是执行字符串替换，请使用转义序列 %%。
<pre>
[MyAddReg]
HKR,,DllPath,%%SystemRoot%%\System32\myDll.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1285:不能指定 [ClassInstall32] 部分，了解 Microsoft 定义的类。</strong></td>
<td>从 Windows 10 开始 IHV 提供 Inf 不允许使用 [ClassInstall32] 中的任何 Microsoft 定义的类 INF。
</td>
</tr>
<tr>
<td><strong>1296:指定与硬件无关的服务</strong></td>
<td>从 Windows 10，版本 1809，开始这已从警告变为错误。  。服务部分所需的每个定义的目标操作系统。  这是很好的做法，适用于所有 Inf 和不只是 1809年。  

如果您以前不包括本部分中没有提供的服务，因此所依赖的收件箱驱动程序服务，然后您可能需要创建。服务引用使用需求的收件箱 INF 服务并包含语句的部分。  

例如：INF 文件可以得到如下结果。服务为每个 OS 目标，若要解决此错误的部分。

<pre>
[XXXXXXXX.Install.NTx86.Services]
Include=filename.inf
Needs=inf-section-name.Services
</pre>

对于不需要功能驱动程序的设备，可以按如下所示指定 NULL 驱动程序：
<pre>
AddService = ,2.
</pre>
<b>仅应使用此 INF 安装的非功能性的设备，若要指定不需要的驱动程序的这种情况。</b>
</td>
</tr>
</tbody>
</table>

## <a name="universal-inf-1300-1319"></a>通用 INF (1300年 1319)

>[!IMPORTANT]
>驱动程序 INF 文件是通用如果范围 13 中未收到任何错误或警告，且错误编号*xx*。

与 INF 可配置性相关的以下错误和警告：

<table>
<thead>
<tr>
<th>错误/警告代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1300:找到旧</strong><em>Xxx</em></td>
<td>如果你使用不推荐使用的部分或指令如，将看到此错误<a href="https://msdn.microsoft.com/library/windows/hardware/ff547448"> <strong>LogConfig</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff547321"> <strong>DDInstall.CoInstallers</strong></a>。</td>
</tr>
<tr>
<td><strong>1301:找到旧</strong><em>Xxx</em><strong>操作</strong><em>Xxx</em></td>
<td>如果你使用不推荐使用的部分或指令如，将看到此错误<a href="https://msdn.microsoft.com/library/windows/hardware/ff547448"> <strong>LogConfig</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff547321"> <strong>DDInstall.CoInstallers</strong></a>。</td>
</tr>
<tr>
<td><strong>1302:找到旧</strong><em>Xxx</em><strong>操作</strong><em>Xxx</em></td>
<td>该操作会影响外部驱动程序包，如删除服务或删除文件的内容时发生此错误。</td>
</tr>
<tr>
<td><strong>1303:找到旧定义共同安装程序的操作</strong></td>
<td>错误 1303年表示 AddReg 操作指定共同安装程序。 例如：
<pre>
AddReg = HKR,,CoInstallers32,0x00010000,"MyCoinstaller.dll"
</pre>
</td>
</tr>
<tr>
<td><strong>1304:找到旧使用非相对密钥的操作</strong></td>
<td>错误 1304年指示注册表操作使用 HKR 以外的注册表根。</td>
</tr>
<tr>
<td><strong>1305:找到旧操作使用可附加的多 sz 值</strong></td>
<td>错误 1305年表示 INF 删除取值<strong>REG_MULTI_SZ</strong>或将一个值追加到现有<strong>REG_MULTI_SZ</strong>。</td>
</tr>
<tr>
<td><strong>1306:找到旧操作具有非系统目标路径</strong></td>
<td>错误 1306年指示文件复制将指定的目标，则不在 %systemroot%。</td>
</tr>
<tr>
<td><strong>1310-1312:适用于需要指令的不正确的部分扩展</strong></td>
<td>需要指令有效地完成所需的部分复制/粘贴到引用部分。  作为基线验证 InfVerif 比较部分的扩展。  这意味着 [DDInstall.Services] [DDInstall.Services] 的其他部分可以仅使用需求指令。</td>
</tr>
<tr>
<td><strong>1313-1314:缺少包括指令</strong></td>
<td>在每个部分中的使用需求指令，都必须有相应的包括指令以引用包含目标部分 INF。  以前需要指令将有效 Include 指令时在另一个 INF 部分。</td>
</tr>
<tr>
<td><strong>133 x:功能错误</strong></td>
<td>多个注册表部分写入到单个全局密钥。 例如，不同的部分可能具有的服务设置不同的服务配置为全局注册表项设置为不同的数据值或指向不同的源文件的目标文件。</td>
</tr>
</tbody>
</table>

## <a name="installation-2000-2999"></a>安装 (2000年-2999)

2000 2999年范围中的问题显示为警告。 可能的值包括以下内容。

<table>
<thead>
<tr>
<th>错误代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>2083:不引用或使用的部分</strong></td>
<td>此警告意味着 INF 文件提供了一个未引用的部分。 安装该驱动程序时，不会评估警告中引用的部分内容。</td>
</tr>
<tr>
<td><strong>2222:旧指令将被忽略。</strong></td>
<td>此警告意味着 INF 指定一个不推荐使用的指令。 安装该驱动程序时，则不计算引用部分的指令。 例如， <a href="https://msdn.microsoft.com/library/windows/hardware/ff547448"> <strong>INF LogConfig 指令</strong></a>不再支持指令，因此下一节会导致此警告。
<pre>
[InstallSection.LogConfigOverride]
LogConfig=LogConfigSection
...
</pre>
有关哪些 INF 指令不推荐使用的信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff547388">INF 指令</a>。</td>
</tr>
<tr>
<td><strong>2223:部分应具有一个体系结构修饰</strong></td>
<td>此警告意味着 INF 文件包含<a href="https://msdn.microsoft.com/library/windows/hardware/ff547454"> <strong>INF 制造商部分</strong></a> ，它指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff547456"><strong>模型部分</strong></a>没有体系结构修饰。 例如，以下 INF 语法会导致警告 2223年:
<pre>
[Manufacturer]
%MfgName% = InstallSection

[InstallSection]
...
</pre>
在安装该驱动程序时，前面的 INF 语法将默认为 x86。
<p>相反，声明所有支持的体系结构，并为每个提供相应的安装部分：</p>
<pre>
[Manufacturer]
%MfgName% = InstallSection, NTX86, NTAMD64

[InstallSection.NTAMD64]
...

[InstallSection.NTX86]
...
</pre>
INF 文件指定适用于 x86 的修饰的节和未修饰的部分，如果您安装您的驱动程序时，将忽略未修饰的部分。</td>
</tr>
</tbody>
</table>
