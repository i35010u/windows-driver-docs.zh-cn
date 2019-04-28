---
title: Ctrpp 任务
description: Windows Driver Kit (WDK) 提供 Ctrpp 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 ctrpp.exe 工具。
ms.assetid: DB457500-5BFF-4488-95EB-EEB3F63947C1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8989e988f12be06b037ecc580c5352b78d201970
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356623"
---
# <a name="ctrpp-task"></a>Ctrpp 任务


Windows Driver Kit (WDK) 提供 Ctrpp 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 ctrpp.exe 工具。 有关使用 ctrpp.exe 信息，请参阅[ **CTRPP**](https://msdn.microsoft.com/library/windows/desktop/aa372128)。

MSBuild 使用 Ctrpp 项发送到 ctrpp.exe Ctrpp 任务的参数。 项目文件中的 Ctrpp 项访问 ctrpp.exe 的项元数据。

下面的示例显示了如何编辑.vcxproj 文件中的元数据。

```XML
<ItemGroup>
    <Ctrpp Include="a.manifest">
      <GenerateHeaderFileForCounter>true</GenerateHeaderFileForCounter>
      <HeaderFileNameForCounter>c:\test\abc.h</HeaderFileNameForCounter>
    </Ctrpp>
</ItemGroup>
```

下面的示例显示了命令行调用：

```
ctrpp.exe –ch "c:\test\abc.h" a.manifest
```

在上面的示例中，MSBuild 调用 ctrpp.exe 上文件 a.manifest，与 **– ch**选项，因为 GenerateHeaderFileForCounter 元数据设置为 true。 此外，MSBuild 使用 HeaderFileNameForCounter 元数据指定的参数 **– ch**选项

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Ctrpp 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具开关</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Source</td>
<td align="left">@(Ctrpp)</td>
<td align="left"></td>
<td align="left">所需的 ITaskItem 参数。 指定要处理的计数器清单。</td>
</tr>
<tr class="even">
<td align="left">AddPrefix</td>
<td align="left">%(Ctrpp.AddPrefix)</td>
<td align="left"><strong>-prefix</strong><em>&lt;prefix&gt;</em></td>
<td align="left">可选的字符串参数。 指定要添加到函数和变量生成的前缀。</td>
</tr>
<tr class="odd">
<td align="left">BackwardCompatibility</td>
<td align="left">%(Ctrpp.BackwardCompatibility)</td>
<td align="left"><strong>-backcompat</strong></td>
<td align="left">可选布尔参数。 生成与 Windows 7 之前的操作系统二进制兼容的代码。</td>
</tr>
<tr class="even">
<td align="left">EnableLegacy</td>
<td align="left">%(Ctrpp.EnableLegacy)</td>
<td align="left"><strong>-Legacy</strong></td>
<td align="left">可选布尔参数。 将还原到以前的 ctrpp 文件。 此开关将使 ctrpp 生成四个输出文件： 两个标头文件、 资源文件和源代码文件。 这会模拟在以前版本的 ctrpp 所发现的行为。 不能与-旧版结合使用-o，-ch，-rc 和前缀选项。</td>
</tr>
<tr class="odd">
<td align="left">GeneratedCounterFilesPath</td>
<td align="left">%(Ctrpp.GeneratedCounterFilesPath)</td>
<td align="left"><strong>-sumPath</strong><em>&lt;path&gt;</em></td>
<td align="left">可选的字符串参数。 指定要生成二进制计数器文件默认的路径。</td>
</tr>
<tr class="even">
<td align="left">GenerateHeaderFileForCounter</td>
<td align="left">%(Ctrpp.GenerateHeaderFileForCounter)</td>
<td align="left"></td>
<td align="left">如果此值设置为 true，它使-ch 开关。</td>
</tr>
<tr class="odd">
<td align="left">HeaderFileNameForCounter</td>
<td align="left">%(Ctrpp.HeaderFileNameForCounter)</td>
<td align="left"><strong>-ch</strong><em>&lt;filename&gt;</em></td>
<td align="left">可选的字符串参数。 生成包含的计数器名称和 id 的标头文件。</td>
</tr>
<tr class="even">
<td align="left">GenerateHeaderFileForProvider</td>
<td align="left">%(Ctrpp.GenerateHeaderFileForProvider)</td>
<td align="left"></td>
<td align="left">如果此值设置为 true，它使-o 开关。</td>
</tr>
<tr class="odd">
<td align="left">HeaderFileNameForProvider</td>
<td align="left">%(Ctrpp.HeaderFileNameForProvider)</td>
<td align="left"><strong>-o</strong><em>&lt;filename&gt;</em></td>
<td align="left">可选的字符串参数。 生成提供程序的标头文件。</td>
</tr>
<tr class="even">
<td align="left">GenerateMemoryRoutines</td>
<td align="left">%(Ctrpp.GenerateMemoryRoutines)</td>
<td align="left"><strong>-MemoryRoutines</strong></td>
<td align="left">可选布尔参数。 生成内存分配和可用的例行模板。</td>
</tr>
<tr class="odd">
<td align="left">GenerateNotificationCallback</td>
<td align="left">%(Ctrpp.GenerateNotificationCallback)</td>
<td align="left"><strong>-NotificationCallback</strong></td>
<td align="left">可选布尔参数。 生成自定义的通知回调模板。 类似于中的"callback"属性&lt;提供程序&gt;元素。</td>
</tr>
<tr class="even">
<td align="left">GenerateResourceSourceFile</td>
<td align="left">%(Ctrpp.GenerateResourceSourceFile)</td>
<td align="left"></td>
<td align="left">如果此值设置为 true，它使-rc 切换。</td>
</tr>
<tr class="odd">
<td align="left">ResourceFileName</td>
<td align="left">%(Ctrpp.ResourceFileName)</td>
<td align="left"><strong>-rc</strong><em>&lt;filename&gt;</em></td>
<td align="left">可选的字符串参数。 生成资源的源文件。</td>
</tr>
<tr class="even">
<td align="left">GenerateSummaryGlobalFile</td>
<td align="left">%(Ctrpp.GeneratedSummaryGlobalFile)</td>
<td align="left"><strong>-summary</strong><em>&lt;path&gt;</em></td>
<td align="left">可选的字符串参数。 生成每个提供程序的二进制计数器文件生成摘要全局文件 GenSumResource.BIN。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**CTRPP**](https://msdn.microsoft.com/library/windows/desktop/aa372128)
