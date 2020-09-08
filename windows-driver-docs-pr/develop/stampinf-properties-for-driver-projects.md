---
ms.assetid: 18A9ACEF-51F8-4BC0-B305-F58287AD321C
title: 驱动程序项目的 Stampinf 属性
description: 设置 Stampinf 工具的属性。 生成驱动程序时，你可以使用 Stampinf 来更新常用的 INF 和 INX 文件指令。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87271fec3b33e0415bcce2804fa4f7972976de71
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210821"
---
# <a name="stampinf-properties-for-driver-projects"></a>驱动程序项目的 Stampinf 属性

设置 [Stampinf](../devtest/stampinf.md) 工具的属性。 生成驱动程序时，你可以使用 Stampinf 来更新常用的 INF 和 INX 文件指令。

## <a name="span-idsetting_stampinf_properties_for_driver_projectsspanspan-idsetting_stampinf_properties_for_driver_projectsspanspan-idsetting_stampinf_properties_for_driver_projectsspansetting-stampinf-properties-for-driver-projects"></a><span id="Setting_Stampinf_properties_for_driver_projects"></span><span id="setting_stampinf_properties_for_driver_projects"></span><span id="SETTING_STAMPINF_PROPERTIES_FOR_DRIVER_PROJECTS"></span>设置驱动程序项目的 Stampinf 属性


1.  打开驱动程序项目的属性页。 在“解决方案资源管理器”中，选择并按住（或右键单击）驱动程序项目，然后选择“属性” 。
2.  在驱动程序项目的属性页中，选择“配置属性”，然后选择“Stampinf”。
3.  设置项目属性。

如果你想要将此属性页添加到你的项目，以便你可以在生成过程中运行 Stampinf，请参阅 [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)和 [Stampinf 任务](../devtest/stampinf.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Stampinf 选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Enable_Architecture"></span><span id="enable_architecture"></span><span id="ENABLE_ARCHITECTURE"></span><strong>启用体系结构</strong></p></td>
<td align="left"><p>对 INX 文件中使用的 $ARCH$ 变量启用替换。 如已启用，则使用为“体系结构”指定的值。 如果指定为“否”，则将删除 $ARCH$ 变量。 例如，“Standard.NT$ARCH$”将变为“Standard.NT”。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Architecture"></span><span id="architecture"></span><span id="ARCHITECTURE"></span><strong>体系结构</strong></p></td>
<td align="left"><p>指定 <em>architecture</em> 字符串来替换 INX 文件中使用的 $ARCH$ 变量。 默认值为 $(InfArch)，它是一个用于在 Visual Studio 中选择当前处于活动状态的配置的宏。 可能的值包括 <strong>x86</strong>、<strong>x64</strong>。 此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-a [</strong><em>architecture</em><strong>]</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_VersionStamp"></span><span id="enable_versionstamp"></span><span id="ENABLE_VERSIONSTAMP"></span><strong>启用版本戳</strong></p></td>
<td align="left"><p>启用版本时间戳。 如启用，“驱动程序版本号”不得为空。 “驱动程序版本号”指定在版本号的 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](../install/inf-driverver-directive.md)"><strong>INF DriverVer 指令</strong></a>中写入的时间。 如果尚未启用，请参阅“驱动程序版本号”下面有关此选项的默认行为描述。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Driver_Version_Number"></span><span id="driver_version_number"></span><span id="DRIVER_VERSION_NUMBER"></span><strong>驱动程序版本号</strong></p></td>
<td align="left"><p>指定在版本号的 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](../install/inf-driverver-directive.md)"><strong>INF DriverVer 指令</strong></a>中写入的时间。 时间格式为 <em>hours.minutes.seconds.milliseconds</em>（例如，11.30.20.15）。 此选项在开发过程中非常有用，因为通过它可以方便地提高驱动程序的版本号。 此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-v [</strong> <em>time</em> <strong>| <em>]</strong>。</p>
<p>若要使用当前时间，请在此参数中指定星号 (</em>)。</p>
<p><em>默认行为：</em></p>
<p>如果未指定“驱动程序版本号”，或者如果“启用版本戳”为“否”或未指定，则 Stampinf 将使用以下版本号值之一：</p>
<ul>
<li><p>如果已设置 STAMPINF_VERSION 环境变量，则 Stampinf 将使用此环境变量指定的版本号值。</p></li>
<li><p>如果未指定 STAMPINF_VERSION 环境变量，则 Stampinf 将从 ntverp.h 文件中提取版本号。</p></li>
</ul>
<div class="alert">
<strong>注意</strong>  默认情况下，在生成驱动程序时，STAMPINF_VERSION 环境变量未设置，除非你已将其设置为系统环境变量。 若要在 Visual Studio 生成环境中指定此环境变量，请参阅<a href="https://docs.microsoft.com/visualstudio/msbuild/how-to-use-environment-variables-in-a-build?view=vs-2015" data-raw-source="[How to: Use Environment Variables in a Build](/visualstudio/msbuild/how-to-use-environment-variables-in-a-build?view=vs-2015)">如何：在生成时使用环境变量</a>。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_DateStamp"></span><span id="enable_datestamp"></span><span id="ENABLE_DATESTAMP"></span><strong>启用日期戳</strong></p></td>
<td align="left"><p>启用日期戳。 如已启用，“驱动程序版本指令日期”不得为空。 如果尚未启用，请参阅“驱动程序版本指令日期”下面有关此选项的默认行为描述。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Driver_Version_Directive_Date"></span><span id="driver_version_directive_date"></span><span id="DRIVER_VERSION_DIRECTIVE_DATE"></span><strong>驱动程序版本指令日期</strong></p></td>
<td align="left"><p>指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](../install/inf-driverver-directive.md)"><strong>INF DriverVer 指令</strong></a>中写入的日期。 日期格式为<em>月</em>/<em>日</em>/<em>年</em>（例如，<strong>10/20/2011</strong>）。</p>
<p>若要使用当前日期，请在此参数中指定星号 (<strong><em></strong>)。</p>
<p><em>默认行为：</em></p>
<p>如果未指定“驱动程序版本指令日期”参数，或者如果“启用日期戳”为“否”或未指定，则 Stampinf 将使用以下日期值之一：</p>
<ul>
<li><p>如果已设置 STAMPINF_DATE 环境变量，则 Stampinf 将使用此环境变量指定的日期值。</p></li>
<li><p>如果未指定 STAMPINF_DATE 环境变量，则 Stampinf 将使用当前日期。</p></li>
</ul>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-d [</strong><em>date</em><strong>|</em>]</strong>。</p>
<div class="alert">
<strong>注意</strong>  默认情况下，在生成驱动程序时，STAMPINF_DATE 环境变量未设置，除非你已将其设置为系统环境变量。 若要在 Visual Studio 生成环境中指定此环境变量，请参阅<a href="https://docs.microsoft.com/visualstudio/msbuild/how-to-use-environment-variables-in-a-build?view=vs-2015" data-raw-source="[How to: Use Environment Variables in a Build](/visualstudio/msbuild/how-to-use-environment-variables-in-a-build?view=vs-2015)">如何：在生成时使用环境变量</a>。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Driver_Version_Directive_Section"></span><span id="driver_version_directive_section"></span><span id="DRIVER_VERSION_DIRECTIVE_SECTION"></span><strong>驱动程序版本指令部分</strong></p></td>
<td align="left"><p>指定要在其中放置 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](../install/inf-driverver-directive.md)"><strong>INF DriverVer 指令</strong></a>的 INF 部分。 此指令所在的默认位置是 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section" data-raw-source="[&lt;strong&gt;INF Version section&lt;/strong&gt;](../install/inf-version-section.md)"><strong>INF Version 部分</strong></a>。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-s</strong> <em>section</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="KMDF_Version_Number"></span><span id="kmdf_version_number"></span><span id="KMDF_VERSION_NUMBER"></span><strong>KMDF 版本号</strong></p></td>
<td align="left"><p>指定此驱动程序依赖的 KMDF 的版本。 这用于自定义 INF 文件中的 KmdfLibraryVersion 和 KMDF 辅助安装程序的名称。 此选项取代了 INF 文件中的 $KMDFVERSION$ 和 $KMDFCOINSTALLERVERSION$ 关键字。 该字符串采用以下格式：</p>
<p><em>&lt;major_version&gt;</em>.<em>&lt;minor_version&gt;</em></p>
<p>例如，如果你将 1.5 指定为版本字符串，则两个关键字将分别使用值 1.5 和 01005。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-k</strong> <em>KMDFversion</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="UMDF_Version_Number"></span><span id="umdf_version_number"></span><span id="UMDF_VERSION_NUMBER"></span><strong>UMDF 版本号</strong></p></td>
<td align="left"><p>指定此驱动程序依赖的 UMDF 的版本。 此选项用于指定 INF 文件中的 UmdfLibraryVersion 和 UMDF 辅助安装程序的名称。 指定的版本 将取代 INF 文件中的 $UMDFVERSION$ 和 $UMDFCOINSTALLERVERSION$ 关键字。 版本字符串采用以下格式：</p>
<p><em>&lt;major_version&gt;</em>.<em>&lt;minor_version&gt;</em>.<em>&lt;service_version&gt;</em></p>
<p>（其中，<em>&lt;service_version&gt;</em> 通常为零）。</p>
<p>例如，如果你将 1.5.0 指定为版本字符串，则最大和最小关键字将分别使用值 1.5.0 和 01005。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-u</strong> <em>UMDFversion</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Catalog_File_Name"></span><span id="catalog_file_name"></span><span id="CATALOG_FILE_NAME"></span><strong>目录文件名</strong></p></td>
<td align="left"><p>指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section" data-raw-source="[&lt;strong&gt;INF Version section&lt;/strong&gt;](../install/inf-version-section.md)"><strong>INF Version 部分</strong></a>中的 <strong>CatalogFile</strong> 指令中写入的值。 默认情况下不写入 <strong>CatalogFile</strong> 指令。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-c</strong> <em>catalogfile</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Verbose"></span><span id="verbose"></span><span id="VERBOSE"></span><strong>详细</strong></p></td>
<td align="left"><p>显示详细的 Stampinf 输出。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-n</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Version_Header_Path"></span><span id="version_header_path"></span><span id="VERSION_HEADER_PATH"></span><strong>版本标头路径</strong></p></td>
<td align="left"><p>指定 Ntverp.h 文件的位置。 此路径表示包含 Ntverp.h 的目录的完全限定路径。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf" data-raw-source="[Stampinf](../devtest/stampinf.md)">Stampinf</a> 选项 <strong>-i</strong> <em>path</em>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [Stampinf](../devtest/stampinf.md)
* [**INF DriverVer 指令**](../install/inf-driverver-directive.md)
* [**INF Version 部分**](../install/inf-version-section.md)
* [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)
* [Stampinf 任务](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786_task)
* [How to:在生成时使用环境变量](/visualstudio/msbuild/how-to-use-environment-variables-in-a-build?view=vs-2015)。
 

