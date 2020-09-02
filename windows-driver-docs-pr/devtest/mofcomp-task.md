---
title: Mofcomp 任务
description: Windows 驱动程序工具包 (WDK) 提供 Mofcomp.exe 任务，以便在使用 MSBuld 构建驱动程序时可以运行 Mofcomp.exe 工具。
ms.assetid: 94B70223-393F-49C9-B2C9-34FF64D26454
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff7f743bc549171b7a374c4e40934688486d0198
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382729"
---
# <a name="mofcomp-task"></a>Mofcomp 任务


Windows 驱动程序工具包 (WDK) 提供 Mofcomp.exe 任务，以便在使用 MSBuld 构建驱动程序时可以运行 Mofcomp.exe 工具。 有关此工具的信息，请参阅 [**mofcomp.exe**](/windows/desktop/WmiSdk/mofcomp)。

MSBuild 使用 Mofcomp.exe 项将 Mofcomp.exe 任务的参数发送到 Mofcomp.exe。 使用项目文件中的 Mofcomp.exe 项访问 Mofcomp.exe 的项元数据。

下面的示例演示如何在 .vcxproj 文件中编辑元数据。

```XML
<ItemGroup>
    <Mofcomp Include="b.mof">
      <WMISyntaxCheck>true</WMISyntaxCheck>
    </Mofcomp>
</ItemGroup>
```

下面的示例演示了命令行调用：

```
mofcomp.exe -WMI b.mof
```

此示例通过-WMI 开关在文件 b. 上调用 mofcomp.exe。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Mofcomp.exe 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具切换</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">源</td>
<td align="left">@ (Mofcomp.exe) </td>
<td align="left"></td>
<td align="left">所需的 ITaskItem [] 参数。 指定源文件的列表。</td>
</tr>
<tr class="even">
<td align="left">改正</td>
<td align="left">% (Mofcomp.exe) </td>
<td align="left"><strong>-修正：</strong><em> &lt; 区域 &gt; 设置</em></td>
<td align="left">可选的字符串参数。 将 MOF 文件拆分成中性语言和特定语言版本。</td>
</tr>
<tr class="odd">
<td align="left">颁发机构</td>
<td align="left">% (Mofcomp.exe) </td>
<td align="left"><strong>-A：</strong><em> &lt; 颁发 &gt; 机构</em></td>
<td align="left">可选的字符串参数。 将 Authority 指定为登录 WMI 时要使用的颁发机构（域名）。</td>
</tr>
<tr class="even">
<td align="left">自动恢复</td>
<td align="left">% (Mofcomp.exe) </td>
<td align="left"><strong>-自动恢复</strong></td>
<td align="left">可选的布尔参数。 将命名 MOF 文件添加到在存储库恢复过程中编译的文件列表中。</td>
</tr>
<tr class="odd">
<td align="left">CreateBinaryMOFFile</td>
<td align="left">% (Mofcomp.exe. CreateBinaryMOFFile) </td>
<td align="left"><strong>-B：</strong><em> &lt; 文件名 &gt; </em></td>
<td align="left">可选的字符串参数。 请求编译器创建具有名称文件名的二进制版本的 MOF 文件，而不会对 WMI 存储库进行任何修改。</td>
</tr>
<tr class="even">
<td align="left">LanguageNeutralOutput</td>
<td align="left">% (Mofcomp.exe. LanguageNeutralOutput) </td>
<td align="left"><strong>-MOF：</strong><em> &lt; 路径 &gt; </em></td>
<td align="left">可选的字符串参数。 中性语言输出的名称。</td>
</tr>
<tr class="odd">
<td align="left">LanguageSpecificOutput</td>
<td align="left">% (Mofcomp.exe. LanguageSpecificOutput) </td>
<td align="left"><strong>-MFL：</strong><em> &lt; Path &gt; </em></td>
<td align="left">可选的字符串参数。 特定语言输出的名称。</td>
</tr>
<tr class="even">
<td align="left">MinimalRebuildFromTracking</td>
<td align="left">% (Mofcomp.exe. MinimalRebuildFromTracking) </td>
<td align="left"></td>
<td align="left">可选的布尔参数。 如果为 true，则执行跟踪的增量生成;否则，将执行重新生成。</td>
</tr>
<tr class="odd">
<td align="left">MOFClass</td>
<td align="left">% (Mofcomp.exe. MOFClass) </td>
<td align="left"><ul>
<li><strong>-class：</strong><em>createonly</em></li>
<li><strong>-class：</strong><em>forceupdate</em></li>
<li><strong>-class：</strong><em>safeupdate</em></li>
<li><strong>-class：</strong><em>updateonly</em></li>
</ul></td>
<td align="left">可选的字符串参数。 允许或禁止在 MOF 文件中创建或更新类。 有关详细信息，请参阅一流系列交换机上的文档。</td>
</tr>
<tr class="even">
<td align="left">MOFInstance</td>
<td align="left">% (Mofcomp.exe. MOFInstance) </td>
<td align="left"><ul>
<li><strong>-instance：</strong><em>createonly</em></li>
<li><strong>-instance：</strong><em>updateonly</em></li>
</ul></td>
<td align="left">可选的字符串参数。 允许在 MOF 文件中创建或更新实例。 有关详细信息，请参阅-instance 系列交换机上的文档。</td>
</tr>
<tr class="odd">
<td align="left">NamespacePath</td>
<td align="left">% (Mofcomp.exe. NamespacePath) </td>
<td align="left"><strong>-N：</strong><em> &lt; namespacepath &gt; </em></td>
<td align="left">可选的字符串参数。 请求编译器将 MOF 文件加载到 namespacepath 指定的命名空间。</td>
</tr>
<tr class="even">
<td align="left">密码</td>
<td align="left">% (Mofcomp.exe) </td>
<td align="left"><strong>-P：</strong><em> &lt; 密码 &gt; </em></td>
<td align="left">可选的字符串参数。 指定密码作为计算机用户登录时要输入的密码。</td>
</tr>
<tr class="odd">
<td align="left">ResourceLocale</td>
<td align="left">% (Mofcomp.exe. ResourceLocale) </td>
<td align="left"><strong>-L：</strong><em> &lt; ResourceLocale &gt; </em></td>
<td align="left">可选的字符串参数。 与 -ER 开关一起使用时，从二进制 MOF 中提取本地化的 MOF 描述。</td>
</tr>
<tr class="even">
<td align="left">ResourceName</td>
<td align="left">% (Mofcomp.exe) </td>
<td align="left"><strong>-ER：</strong><em> &lt; context.resourcename &gt; </em></td>
<td align="left">可选的字符串参数。 从命名资源中提取二进制 MOF。</td>
</tr>
<tr class="odd">
<td align="left">SyntaxCheck</td>
<td align="left">% (Mofcomp.exe. SyntaxCheck) </td>
<td align="left"><strong>-check</strong></td>
<td align="left">可选的布尔参数。 请求编译器仅执行语法检查并打印相应的错误消息。 此开关不能使用其他开关。</td>
</tr>
<tr class="even">
<td align="left">ToolPath</td>
<td align="left">$ (MofcompToolPath) </td>
<td align="left"></td>
<td align="left">可选的字符串参数。 允许您指定该工具所在的文件夹的完整路径。</td>
</tr>
<tr class="odd">
<td align="left">TrackerLogDirectory</td>
<td align="left">% (Mofcomp.exe. TrackerLogDirectory) </td>
<td align="left"></td>
<td align="left">可选的字符串参数。 指定跟踪器用于写入 tlog 的日志目录。</td>
</tr>
<tr class="even">
<td align="left">TrackFileAccess</td>
<td align="left">$ (TrackFileAccess) </td>
<td align="left"></td>
<td align="left">可选的布尔参数。 如果为 true，则跟踪此任务的文件访问模式。</td>
</tr>
<tr class="odd">
<td align="left">UserName</td>
<td align="left">% (Mofcomp.exe) </td>
<td align="left"><strong>-U：</strong><em> &lt; 用户名 &gt; </em></td>
<td align="left">可选的字符串参数。 指定用户名作为登录用户的名称。</td>
</tr>
<tr class="even">
<td align="left">WMISyntaxCheck</td>
<td align="left">% (Mofcomp.exe. WMISyntaxCheck) </td>
<td align="left"><strong>-WMI</strong></td>
<td align="left">可选的布尔参数。 请求编译器执行 WMI 语法检查。 -B：开关必须与此开关一起使用。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**mofcomp**](/windows/desktop/WmiSdk/mofcomp)

 

