---
title: INF 验证错误和警告
description: Microsoft Visual Studio 执行的自动 INF 验证会导致驱动程序安装错误和警告。
ms.date: 03/04/2021
ms.localizationpriority: medium
ms.openlocfilehash: 348eda2466333b1f4d79f129a14bb30985b12496
ms.sourcegitcommit: 0cdf5984551c519acbfa3557845df55206dd4ee3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104761260"
---
# <a name="inf-validation-errors-and-warnings"></a>INF 验证错误和警告

本主题介绍了驱动程序安装错误，以及可作为 Microsoft Visual Studio 执行的自动 INF 验证或运行 [InfVerif](infverif.md) 工具时显示的警告。

从带有 WDK 10 的 Visual Studio 2015 开始，当你构建驱动程序时，"错误列表" 窗格中会出现以下 INF 文件错误。 如果从命令行运行 InfVerif.exe，则该工具会在命令提示符下或在 HTML 版本的结果中显示这些错误。

## <a name="error-guidance"></a>错误指南

InfVerif 遵循错误号越低的一般规则，问题就越严重。
大多数错误代码可以是警告或错误，具体取决于提供给 InfVerif 的参数。

### <a name="handling-errors"></a>处理错误

必须解决所有错误才能在硬件开发人员中心仪表板上传递驱动程序测试。 错误与以下条件相关：

- INF 分析器无法成功解释 INF
- INF 分析器只能通过使默认值假设 (不明确的语法来解释 INF) 
- InfVerif 的参数指示规则集应应用于 INF (例如通用) 

尽管在开发人员中心提交驱动程序之前不需要修复警告，但建议花时间了解所报告的问题。 如果你不知道给定的警告，则 INF 可能并非始终按预期方式工作。

警告通常与相关：

- 语法不正确，但具有适当的有效方案
- 对给定的 InfVerif 参数有效但在其他模式（如通用）中出错的语法

如果出现以下情况，则与通用设置相关的问题将显示为错误：

- 在 Visual Studio 中，会生成驱动程序，并将目标平台设置为 " **通用** " 或 " **移动**"。
- 从命令行运行 InfVerif.exe 并指定/u 标志。

如果出现以下情况，则与通用设置相关的问题将显示为警告：

- 在 Visual Studio 中，会生成驱动程序，并将目标平台设置为 " **桌面**"。
- 您从命令行运行 InfVerif.exe，而不指定/u 标志。

## <a name="error-codes"></a>错误代码

错误代码分为以下几个类别：

- [INF 文件中的语法 (1100-1299) ](#syntax-in-the-inf-file-1100-1299)
- [通用 INF (1300-1319) ](#universal-inf-1300-1319)
- [Windows 驱动程序 (1320-1329) ](#windows-driver-1320-1329)
- [安装 (2000-2999) ](#installation-2000-2999)

并非所有错误代码都列在下面，因为许多错误代码都有一目了然的含义。 1000-1099 范围内的错误被视为一目了然，因为它们是基本的语法错误。

## <a name="syntax-in-the-inf-file-1100-1299"></a>INF 文件中的语法 (1100-1299) 

尽管 InfVerif 故障意味着驱动程序提交失败，驱动程序安装仍可能会成功。
这是因为，在安装驱动程序时，如果 INF 文件中存在错误，Windows 也会尝试设置的默认值。
由于此范围内的错误，Windows 不会导致驱动程序安装失败，但在此范围内的错误表示此行为可能会因操作系统版本或 SKU 而异。
如果驱动程序安装成功，这些错误表明存在驱动程序可能安装不 *正确的情况* 。

<table>
<thead>
<tr>
<th>错误代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1100： DriverStore Copyfile 名称不匹配</strong></td>
<td>如果将文件从其原始驱动程序存储名称和位置重命名为驱动程序存储区中的其他名称和位置，将出现此错误。  例如：
<pre>
[SourceDisksFiles]
DriverFile.sys=1,x64  

[DestinationDirs]
CopyFileSection=13,SubDirectory  
  
[CopyFileSection]
DriverFile.sys
</pre>
驱动程序存储区维护原始驱动程序包目录结构。  在上面的代码中，DriverFile.sys 的原始位置是 <i>inf location</i>\x64，但 CopyFiles 指令将它放在 <i>inf 位置</i>\SubDirectory。  如果在复制过程中重命名了该文件，则会显示相同的错误。</td>
</tr>
<tr>
<td><strong>1203：找不到节</strong></td>
<td>例如，以下 INF 语法导致错误1203：
<pre>
[MyInstallSection]
CopyFiles=driverFile.sys
</pre>
报告此错误的原因是 <strong>CopyFiles</strong> 指令需要一个 (的节名称，该名称指定要复制) 的文件的列表。 但是， <strong>CopyFiles</strong> 指令可以指定文件名。 若要区分部分名称和文件名，请在文件名前加上 @ 标记，如下所示：
<pre>
[MyInstallSection]
CopyFiles=@driverFile.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1204：提供程序不能为 Microsoft</strong></td>
<td>[Version] 部分中的 "提供程序" 字段无法指定 Microsoft。
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
<td><strong>1205：从 [Directive1] 和 [Directive2] 指令引用的节 [Driver_files]</td>
<td>只要两个不同指令指向同一节，就会生成此警告。
  <p>请注意，在大多数情况下，这实际上是一个错误，在某些情况下会报告1205，即使条件已启用也是如此。</td>
</tr>
<tr>
<td><strong>1212：不能同时拥有 [DefaultInstall] 和 [Manufacturer]</strong></td>
<td>单个 INF 不能同时包含 [DefaultInstall] 和 [Manufacturer]。  用这二者编写的 Inf 应删除这两个部分中的一个。
</td>
</tr>
<tr>
<td><strong>1220：无法直接引用包含的 INF 中定义的节</strong></td>
<td>如果 INF 文件引用了包含的 INF 中的 <a href="/windows-hardware/drivers/install/inf-ddinstall-section">DDInstall</a> 部分，则必须使用 " <strong>需要</strong> " 指令。 从包含的 INF 引用节的任何其他指令都会导致错误1220。
<p>在此示例中，.INF 的 "安装" 部分引用了 .INF 中的等效安装部分。</p>
<p>.INF 包含：</p>
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
<p>B. .INF 包含：</p>
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
<p><strong>需要</strong>指令必须引用要在当前安装部分中处理的等效安装部分。 例如，[InstallSectionA] 中的需要指令应指向。其他安装部分的服务。 还可以使用 " <strong>需要</strong> " 指令来包括同一 INF 中其他 DDInstall 部分的行为。 对其他类型的节使用 " <strong>需要</strong> " 指令可能会导致意外的行为。</p></td>
</tr>
<tr>
<td><strong>1221：无法修改服务 regkey，必须使用 HKR</strong></td>
<td>此错误表示 INF 文件引用了服务注册表项中的位置，例如 <strong> HKLM\SYSTEM\CurrentControlSet\Services &lt; Em &gt; 服务名称 </em></strong> 。 访问服务密钥时，应改为使用相对根 (<strong>HKR</strong>) 将注册表值与设备或驱动程序实例相关联。
<p>当你使用 <strong>HKR</strong>时，在安装设备之前，将不会显示该注册表值。</p></td>
</tr>
<tr>
<td><strong>1230： [SourceDisksFiles] 部分下缺少文件 "xxxx"。</strong></td>
<td>这表示已将文件指定为驱动程序包的一部分，但在 [SourceDisksFiles] 节中未指定与 INF 相关的文件的源位置。
<pre>
[SourceDisksFiles]
filename=disk id
</pre>
请注意，如果为 [SourceDisksFiles] 指定了体系结构修饰版本 (如 [SourceDisksFiles]），则经常会发生此错误，但 INF 不支持的所有体系结构都有 [SourceDisksFiles] 部分。</td>
</tr>
<tr>
<td><strong>1233：缺少签名所需的指令</strong></td>
<td>在 [Version] 部分中，你必须指定 CatalogFile 指令 (和关联的目录文件) 才能接收驱动程序包上的签名。
<pre>
CatalogFile=wudf.cat
</pre>
</td>
</tr>
<tr>
<td><strong>1235：未在 [字符串] 中定义字符串标记</strong></td>
<td>指定的字符串标记在 [字符串] 部分没有定义。 例如，INF 文件在<a href="/windows-hardware/drivers/install/inf-addreg-directive"><strong>AddReg</strong></a>指令指定的 "<em>外接程序" 部分</em>中指定<em>% REG_DWORD%</em> ，但在<a href="/windows-hardware/drivers/install/inf-strings-section">[string]</a>部分中没有对应的 REG_DWORD = 0x00010001。
<p>如果 INF 文件指定了包含环境变量的注册表值，则会经常发生此错误。 例如：</p>
<pre>
[MyAddReg]
HKR,,DllPath,%SystemRoot%\System32\myDll.sys
</pre>
此行使 INF 分析器尝试从 [String] 部分查找令牌 "SystemRoot"，而不是在注册表中存储文本 "% SystemRoot%" 的预期行为。  若要使用文本值% SystemRoot% 而不是执行字符串替换，请使用转义序列%%。
<pre>
[MyAddReg]
HKR,,DllPath,%%SystemRoot%%\System32\myDll.sys
</pre>
</td>
</tr>
<tr>
<td><strong>1285：无法为 Microsoft 定义的类指定 [ClassInstall32] 部分。</strong></td>
<td>在 Windows 10 中，不允许 IHV 提供的 Inf 在任何 Microsoft 定义的类的 INF 中使用 [ClassInstall32]。
</td>
</tr>
<tr>
<td><strong>1296：指定的服务与硬件不关联</strong></td>
<td>从 Windows 10 版本1809开始，此问题已从警告更改为错误。  此.每个定义的目标 OS 都需要服务节。  这是一种很好的做法，适用于所有 Inf，而不仅仅适用于1809。  

如果之前未包括此部分，因为没有服务，并且依赖于收件箱驱动程序服务，则可能需要创建。使用 "需要" 和 "包含" 声明引用收件箱 INF 的服务的服务部分。  

例如： INF 文件具有以下内容。每个 OS 目标的服务部分以解决此错误。

<pre>
[XXXXXXXX.Install.NTx86.Services]
Include=filename.inf
Needs=inf-section-name.Services
</pre>

对于不需要函数驱动程序的设备，可以按如下所示指定 NULL 驱动程序：
<pre>
AddService = ,2
</pre>

<b>仅在 INF 正在安装非功能性设备以指定它不需要驱动程序时才使用此方法。</b>

例如：只需筛选器驱动程序，而不需要函数驱动程序的设备会有两个 AddService 指令：
<pre>
AddService = MyFilterDriver,, My-Service-Install-Section 
AddService = ,2
</pre>

</td>
</tr>
<tr>
<td><strong>1297：设备驱动程序未安装在任何设备上，请使用基元驱动程序（如果适用）。</strong></td>
<td>这表明 INF 文件是设备驱动程序，但未用作设备驱动程序。 这可能会导致驱动程序存储区如何处理驱动程序中的问题。 如果不是这种情况，请检查 INF 以确保正确指定硬件 Id。 如果不打算在设备上安装驱动程序，请将其转换为基元驱动程序。  有关详细信息，请参阅 <a href="/windows-hardware/drivers/develop/creating-a-primitive-driver#converting-from-a-device-driver-inf">从设备驱动程序 INF 转换</a>。
</td>
</tr>
</tbody>
</table>

## <a name="universal-inf-1300-1319"></a>通用 INF (1300-1319) 

>[!IMPORTANT]
>如果未在 13 *00*-13 *19* 范围内收到错误号或警告，则驱动程序 INF 文件是通用的。

以下错误和警告与 INF 可配置性相关：

<table>
<thead>
<tr>
<th>错误/警告代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1300：发现旧</strong><em>Xxx</em></td>
<td>如果使用不推荐使用的节或指令（如 <a href="/windows-hardware/drivers/install/inf-logconfig-directive"><strong>LogConfig</strong></a> 或 <a href="/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section"><strong>DDInstall</strong></a>），则会看到此错误。</td>
</tr>
<tr>
<td><strong>1301：发现旧</strong><em>xxx</em><strong>操作</strong><em>xxx</em></td>
<td>如果使用不推荐使用的节或指令（如 <a href="/windows-hardware/drivers/install/inf-logconfig-directive"><strong>LogConfig</strong></a> 或 <a href="/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section"><strong>DDInstall</strong></a>），则会看到此错误。</td>
</tr>
<tr>
<td><strong>1302：已找到</strong><em>xxx</em>的旧版<em>Xxx</em><strong>操作</strong></td>
<td>当操作影响驱动程序包的外部内容（如删除服务或删除文件）时，会出现此错误。</td>
</tr>
<tr>
<td><strong>1303：找到了定义共同安装程序的旧式操作</strong></td>
<td>错误1303表示 AddReg 操作正在指定 coinstaller。 例如：
<pre>
AddReg = HKR,,CoInstallers32,0x00010000,"MyCoinstaller.dll"
</pre>
</td>
</tr>
<tr>
<td><strong>1304：使用非相对键找到了旧操作</strong></td>
<td>错误1304表示注册表操作使用除 HKR 以外的注册表根目录。</td>
</tr>
<tr>
<td><strong>1305：使用可追加的多 sz 值找到了旧操作</strong></td>
<td>错误1305指示 INF 从 <strong>REG_MULTI_SZ</strong> 中删除值或向现有 <strong>REG_MULTI_SZ</strong>追加值。</td>
</tr>
<tr>
<td><strong>1306：找到了具有非系统目标路径的旧式操作</strong></td>
<td>错误1306表示文件复制指定的目标不在% SystemRoot% 下。</td>
</tr>
<tr>
<td><strong>1310-1312：需求指令的部分扩展不正确</strong></td>
<td>需要指令有效地将所需部分复制/粘贴到引用部分。  作为基准验证，InfVerif 会比较部分的扩展。  这意味着 [DDInstall] 只能对其他 [DDInstall] 部分使用 "需要" 指令。</td>
</tr>
<tr>
<td><strong>1313-1314：缺少包含指令</strong></td>
<td>在使用 "需要" 指令的每个部分中，必须有相应的包含指令，才能引用包含目标部分的 INF。  如果 Include 指令在另一个 INF 部分中，则需要指令将是有效的。</td>
</tr>
<tr>
<td><strong>133x：功能错误</strong></td>
<td>多个注册表节写入一个全局键。 例如，不同的部分可能会将服务设置为不同的服务配置，将全局注册表项设置为不同的数据值，或者将目标文件指向不同的源文件。</td>
</tr>
</tbody>
</table>

## <a name="windows-driver-1320-1329"></a>Windows 驱动程序 (1320-1329) 

>[!IMPORTANT]
>如果未在 13 *2x* 范围内收到错误号或警告，则驱动程序 INF 文件符合 Windows 驱动程序要求。 <a href="/windows-hardware/drivers/develop/driver-isolation"><strong>驱动程序隔离要求</strong></a>文档中详细介绍了这些要求。

以下错误和警告与 Windows 驱动程序要求相关：

<table>
<thead>
<tr>
<th>错误/警告代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>1320：不会将注册表根 <em>Xxx</em> 隔离到 HKR</strong></td>
<td>错误1320表示注册表项操作不符合 <a href="/windows-hardware/drivers/develop/driver-isolation#reading-and-writing-state"><strong>读写状态</strong></a>中定义的注册表要求。
</td>
</tr>
<tr>
<td><strong>1321：值为<em>xxx</em>的注册表根<em>Xxx</em>未隔离到 HKR</strong></td>
<td>错误1321表示注册表值操作不符合 <a href="/windows-hardware/drivers/develop/driver-isolation#reading-and-writing-state"><strong>读写状态</strong></a>中定义的注册表要求。
</td>
</tr>
<tr>
<td><strong>1322： file <em>xxx</em>的目标文件路径<em>xxx</em>未隔离到 DIRID 13</strong></td>
<td>错误1322表示根据 <a href="/windows-hardware/drivers/develop/driver-isolation#run-from-driver-store"><strong>从驱动程序存储区</strong></a>中定义的要求，将文件复制到无效的目标。
</td>
</tr>
<tr>
<td><strong>1323：服务注册表项 <em>Xxx</em> 必须位于 Parameters 子项下</strong></td>
<td>错误1323表示在参数子项下，根据 <a href="/windows-hardware/drivers/develop/driver-isolation#service-registry-state"><strong>服务注册表状态</strong></a>中定义的要求，不会将服务注册表值设置为 HKR。
</td>
</tr>
<tr>
<td><strong>1324： [Version] 部分应指定 PnpLockdown = 1</strong></td>
<td>错误1324表示版本部分中未指定 PnpLockdown。 此规范将导致 PNP 将额外的安全性添加到驱动程序包中的二进制文件，以防止篡改并应始终在驱动程序包中指定。
</td>
</tr>
</tbody>
</table>

## <a name="installation-2000-2999"></a>安装 (2000-2999) 

2000-2999 范围内的问题显示为警告。 可能的值包括以下值。

<table>
<thead>
<tr>
<th>错误代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>2083：未引用或使用的节</strong></td>
<td>此警告指示 INF 文件提供未引用的部分。 安装驱动程序时，不会评估在警告中引用的部分的内容。</td>
</tr>
<tr>
<td><strong>2222：将忽略旧指令。</strong></td>
<td>此警告指示 INF 指定了一个不推荐使用的指令。 安装驱动程序时，不会计算引用节的指令。 例如，不再支持 <a href="/windows-hardware/drivers/install/inf-logconfig-directive"><strong>INF LogConfig 指令</strong></a> 指令，因此以下部分会生成此警告。
<pre>
[InstallSection.LogConfigOverride]
LogConfig=LogConfigSection
...
</pre>
有关弃用了哪些 INF 指令的信息，请参阅 <a href="/windows-hardware/drivers/install/inf-directives">Inf 指令</a>。</td>
</tr>
<tr>
<td><strong>2223：节应具有体系结构修饰</strong></td>
<td>此警告指示 INF 文件包含一个 " <a href="/windows-hardware/drivers/install/inf-manufacturer-section"><strong>Inf 制造商" 部分</strong></a> ，该部分指定了不包含体系结构修饰的 <a href="/windows-hardware/drivers/install/inf-models-section"><strong>模型部分</strong></a> 。 例如，以下 INF 语法将导致警告2223：
<pre>
[Manufacturer]
%MfgName% = InstallSection

[InstallSection]
...
</pre>
安装该驱动程序时，前面的 INF 语法默认为 "x86"。
<p>相反，请声明所有支持的体系结构，并为每个体系结构提供相应的安装部分：</p>
<pre>
[Manufacturer]
%MfgName% = InstallSection, NTX86, NTAMD64

[InstallSection.NTAMD64]
...

[InstallSection.NTX86]
...
</pre>
如果 INF 文件指定了 x86 的修饰部分和未修饰的节，则在安装驱动程序时将忽略未修饰的部分。</td>
</tr>
</tbody>
</table>
