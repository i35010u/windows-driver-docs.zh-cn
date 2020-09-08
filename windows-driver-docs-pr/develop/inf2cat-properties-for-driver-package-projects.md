---
ms.assetid: 0877831F-2FBF-402E-A01B-B153F2A18AD4
title: 驱动程序包项目的 Inf2Cat 属性
description: 设置 Inf2Cat 工具的属性。 Inf2Cat 工具可用于为具有 INF 文件的任何驱动程序包创建目录文件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f61ecd40cf7a42c96976b30de53d84647aa2c7f4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215652"
---
# <a name="inf2cat-properties-for-driver-package-projects"></a>驱动程序包项目的 Inf2Cat 属性

设置 [**Inf2Cat**](../devtest/inf2cat.md) 工具的属性。 **Inf2Cat** 工具可用于为具有 INF 文件的任何驱动程序包创建目录文件。

## <a name="span-idsetting_inf2cat_properties_for_driver_package_projectsspanspan-idsetting_inf2cat_properties_for_driver_package_projectsspanspan-idsetting_inf2cat_properties_for_driver_package_projectsspansetting-inf2cat-properties-for-driver-package-projects"></a><span id="Setting_Inf2Cat_properties_for_driver_package_projects"></span><span id="setting_inf2cat_properties_for_driver_package_projects"></span><span id="SETTING_INF2CAT_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>设置驱动程序包项目的 Inf2Cat 属性


1.  打开驱动程序包的属性页。 在“解决方案资源管理器”中，选择并按住（或右键单击）驱动程序包项目，然后选择“属性”。
2.  在驱动程序包的属性页中，选择“配置属性”，然后选择“Inf2Cat”。
3.  选择“运行 Inf2Cat”  选项。 此选项将在项目中的任何 INF 文件（例如 .inf、.inx 或 .inv 文件）上运行 [**Inf2Cat**](../devtest/inf2cat.md) 工具。

如果驱动程序包是通过 INF 文件安装，则可使用 Inf2Cat 工具来创建目录文件。 Inf2Cat 用于验证 INF 文件中引用的文件是否存在于程序包中。 若要将文件添加到程序包，请使用程序包项目和驱动程序项目的属性页。 有关详细信息，请参阅[创建驱动程序包](creating-a-driver-package.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Run_Inf2Cat"></span><span id="run_inf2cat"></span><span id="RUN_INF2CAT"></span><strong>运行 Inf2Cat</strong></p></td>
<td align="left"><p>在项目中的任何 INF 文件（例如 .inf、.inx 或 .inv 文件）上运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 工具。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Windows_Version_List"></span><span id="windows_version_list"></span><span id="WINDOWS_VERSION_LIST"></span><strong>Windows 版本列表</strong></p></td>
<td align="left"><p>指定 .inf 文件支持的 Windows 版本列表。 使用逗号分隔每个 Windows 版本。 默认设置为 $(Inf2CatWindowsVersionList)，此宏可以为活动平台和配置生成驱动程序。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/os:</strong><em>WindowsVersionList</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Include_Page_Hashes"></span><span id="include_page_hashes"></span><span id="INCLUDE_PAGE_HASHES"></span><strong>包含页面哈希</strong></p></td>
<td align="left"><p>在文件中包含页面哈希。 可选择性地后跟文件列表。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/pageHashes[:</strong><em>file1</em><strong>][,</strong><em>file2</em><strong>]...]</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Add_PE_Attribute"></span><span id="add_pe_attribute"></span><span id="ADD_PE_ATTRIBUTE"></span><strong>添加 PE 属性</strong></p></td>
<td align="left"><p>为文件添加 PE 目录属性。 可选择性地后跟文件列表。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/pe[:</strong><em>file1</em><strong>[,</strong><em>file2</em><strong>]...]</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Add_Drm"></span><span id="add_drm"></span><span id="ADD_DRM"></span><strong>添加 Drm</strong></p></td>
<td align="left"><p>为文件添加 DRM 级别目录属性。 可选择性地后跟文件列表。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/drm[:</strong><em>file1</em><strong>[,</strong><em>file2</em><strong>]...]</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verbose"></span><span id="verbose"></span><span id="VERBOSE"></span><strong>详细</strong></p></td>
<td align="left"><p>显示与 Visual Studio 输出窗口中的工具输出相关的详细信息。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/verbose</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="No_Catalog"></span><span id="no_catalog"></span><span id="NO_CATALOG"></span><strong>无目录</strong></p></td>
<td align="left"><p>防止创建任何目录文件。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/nocat</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Use_Local_Time"></span><span id="use_local_time"></span><span id="USE_LOCAL_TIME"></span><strong>使用本地时间</strong></p></td>
<td align="left"><p>在验证 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer Directive&lt;/strong&gt;](../install/inf-driverver-directive.md)"><strong>INF DriverVer Directive</strong></a> 指令时使用本地时区。 默认情况下使用 UTC。</p>
<p>此设置相当于指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 选项 <strong>/uselocaltime</strong>。</p></td>
</tr>
</tbody>
</table>

 

有关 Inf2Cat 工具的详细信息，请参阅[使用 Inf2Cat 创建目录文件](../install/using-inf2cat-to-create-a-catalog-file.md)。

有关属性页和项目的信息，请参阅 [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [为 PnP 驱动程序包创建目录文件](../install/creating-a-catalog-file-for-a-pnp-driver-package.md)
* [**Inf2Cat**](../devtest/inf2cat.md)
* [创建驱动程序包](creating-a-driver-package.md)
* [签署驱动程序](signing-a-driver.md)
* [使用 Inf2Cat 创建目录文件](../install/using-inf2cat-to-create-a-catalog-file.md)
* [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)
 

