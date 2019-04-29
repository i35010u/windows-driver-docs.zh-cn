---
title: Mofcomp 任务
description: Windows Driver Kit (WDK) 提供 Mofcomp 任务，以便在生成使用 MSBuld 驱动程序时，可以运行 Mofcomp.exe 工具。
ms.assetid: 94B70223-393F-49C9-B2C9-34FF64D26454
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b2bb65b55b3f843e92d1c344af62b8faaf28ebc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391328"
---
# <a name="mofcomp-task"></a>Mofcomp 任务


Windows Driver Kit (WDK) 提供 Mofcomp 任务，以便在生成使用 MSBuld 驱动程序时，可以运行 Mofcomp.exe 工具。 有关工具的信息，请参阅[ **mofcomp**](https://msdn.microsoft.com/library/aa392389)。

MSBuild 使用 Mofcomp 项发送到 Mofcomp.exe Mofcomp 任务的参数。 在项目文件中使用 Mofcomp 项访问 Mofcomp 的项元数据。

下面的示例显示了如何编辑.vcxproj 文件中的元数据。

```XML
<ItemGroup>
    <Mofcomp Include="b.mof">
      <WMISyntaxCheck>true</WMISyntaxCheck>
    </Mofcomp>
</ItemGroup>
```

下面的示例显示了命令行调用：

```
mofcomp.exe -WMI b.mof
```

此示例调用上使用-WMI 开关文件 b.mof mofcomp.exe。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Mofcomp 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具开关</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">源</td>
<td align="left">@(Mofcomp)</td>
<td align="left"></td>
<td align="left">必需的 ITaskItem [] 参数。 指定源文件的列表。</td>
</tr>
<tr class="even">
<td align="left">修正合同</td>
<td align="left">%(Mofcomp.Amendment)</td>
<td align="left"><strong>-修正合同：</strong><em>&lt;区域设置&gt;</em></td>
<td align="left">可选的字符串参数。 将 MOF 文件拆分成中性语言和特定语言版本。</td>
</tr>
<tr class="odd">
<td align="left">颁发机构</td>
<td align="left">%(Mofcomp.Authority)</td>
<td align="left"><strong>-A:</strong><em>&lt;颁发机构&gt;</em></td>
<td align="left">可选的字符串参数。 将 Authority 指定为登录 WMI 时使用的颁发机构（域名）。</td>
</tr>
<tr class="even">
<td align="left">AutoRecover</td>
<td align="left">%(Mofcomp.AutoRecover)</td>
<td align="left"><strong>-autorecover</strong></td>
<td align="left">可选布尔参数。 将命名 MOF 文件添加到在存储库恢复过程中编译的文件列表中。</td>
</tr>
<tr class="odd">
<td align="left">CreateBinaryMOFFile</td>
<td align="left">%(Mofcomp.CreateBinaryMOFFile)</td>
<td align="left"><strong>-B:</strong><em>&lt;文件名&gt;</em></td>
<td align="left">可选的字符串参数。 编译器创建具有名为 MOF 文件的二进制版本而无需对 WMI 存储库进行任何修改的请求。</td>
</tr>
<tr class="even">
<td align="left">LanguageNeutralOutput</td>
<td align="left">%(Mofcomp.LanguageNeutralOutput)</td>
<td align="left"><strong>-MOF:</strong><em>&lt;路径&gt;</em></td>
<td align="left">可选的字符串参数。 中性语言输出的名称。</td>
</tr>
<tr class="odd">
<td align="left">LanguageSpecificOutput</td>
<td align="left">%(Mofcomp.LanguageSpecificOutput)</td>
<td align="left"><strong>-MFL:</strong><em>&lt;路径&gt;</em></td>
<td align="left">可选的字符串参数。 特定语言输出的名称。</td>
</tr>
<tr class="even">
<td align="left">MinimalRebuildFromTracking</td>
<td align="left">%(Mofcomp.MinimalRebuildFromTracking)</td>
<td align="left"></td>
<td align="left">可选布尔参数。 如果为 true，则执行跟踪的增量生成;否则，执行重新生成。</td>
</tr>
<tr class="odd">
<td align="left">MOFClass</td>
<td align="left">%(Mofcomp.MOFClass)</td>
<td align="left"><ul>
<li><strong>-类：</strong><em>createonly</em></li>
<li><strong>-类：</strong><em>forceupdate</em></li>
<li><strong>-类：</strong><em>safeupdate</em></li>
<li><strong>-类：</strong><em>updateonly</em></li>
</ul></td>
<td align="left">可选的字符串参数。 允许或禁止所创建或更新的 MOF 文件中的类。 请参阅文档的详细信息开关-类系列上。</td>
</tr>
<tr class="even">
<td align="left">MOFInstance</td>
<td align="left">%(Mofcomp.MOFInstance)</td>
<td align="left"><ul>
<li><strong>实例：</strong><em>createonly</em></li>
<li><strong>实例：</strong><em>updateonly</em></li>
</ul></td>
<td align="left">可选的字符串参数。 允许创建或更新在 MOF 文件中的实例。 请参阅的文档上的开关的详细信息-实例系列。</td>
</tr>
<tr class="odd">
<td align="left">NamespacePath</td>
<td align="left">%(Mofcomp.NamespacePath)</td>
<td align="left"><strong>-N:</strong><em>&lt;namespacepath&gt;</em></td>
<td align="left">可选的字符串参数。 编译器将 MOF 文件加载到作为 namespacepath 指定的命名空间的请求。</td>
</tr>
<tr class="even">
<td align="left">密码</td>
<td align="left">%(Mofcomp.Password)</td>
<td align="left"><strong>-P:</strong><em>&lt;密码&gt;</em></td>
<td align="left">可选的字符串参数。 指定密码作为计算机用户登录时输入的密码。</td>
</tr>
<tr class="odd">
<td align="left">ResourceLocale</td>
<td align="left">%(Mofcomp.ResourceLocale)</td>
<td align="left"><strong>-L:</strong><em>&lt;ResourceLocale&gt;</em></td>
<td align="left">可选的字符串参数。 使用 -ER 开关时，从二进制 MOF 中提取本地化的 MOF 描述。</td>
</tr>
<tr class="even">
<td align="left">ResourceName</td>
<td align="left">%(Mofcomp.ResourceName)</td>
<td align="left"><strong>-ER:</strong><em>&lt;ResourceName&gt;</em></td>
<td align="left">可选的字符串参数。 从命名资源中提取二进制 MOF。</td>
</tr>
<tr class="odd">
<td align="left">SyntaxCheck</td>
<td align="left">%(Mofcomp.SyntaxCheck)</td>
<td align="left"><strong>-check</strong></td>
<td align="left">可选布尔参数。 请求编译器仅执行语法检查并打印相应的错误消息。 使用此开关可以不使用任何其他开关。</td>
</tr>
<tr class="even">
<td align="left">ToolPath</td>
<td align="left">$(MofcompToolPath)</td>
<td align="left"></td>
<td align="left">可选的字符串参数。 可以指定该工具所在的文件夹的完整路径。</td>
</tr>
<tr class="odd">
<td align="left">TrackerLogDirectory</td>
<td align="left">%(Mofcomp.TrackerLogDirectory)</td>
<td align="left"></td>
<td align="left">可选的字符串参数。 指定跟踪器编写 tlog 的日志目录。</td>
</tr>
<tr class="even">
<td align="left">TrackFileAccess</td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
<td align="left">可选布尔参数。 如果为 true，则跟踪文件访问模式，此任务。</td>
</tr>
<tr class="odd">
<td align="left">UserName</td>
<td align="left">%(Mofcomp.UserName)</td>
<td align="left"><strong>-U:</strong><em>&lt;用户名&gt;</em></td>
<td align="left">可选的字符串参数。 指定在登录的用户的名称作为用户名。</td>
</tr>
<tr class="even">
<td align="left">WMISyntaxCheck</td>
<td align="left">%(Mofcomp.WMISyntaxCheck)</td>
<td align="left"><strong>-WMI</strong></td>
<td align="left">可选布尔参数。 编译器执行 WMI 语法检查的请求。 -B： 必须使用此开关使用开关。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**mofcomp**](https://msdn.microsoft.com/library/aa392389)

 

 






