---
title: V4 打印机驱动程序本地化
description: Windows 8 提供了支持的打印机扩展和 UWP 的设备应用程序开发的标准的、 已本地化的显示字符串。
ms.assetid: 5C587AF2-C51E-4728-A214-7FC1F8A6E445
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31cffd917fad5cda53ba8ad4de2619720ee9bd32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358581"
---
# <a name="v4-printer-driver-localization"></a>V4 打印机驱动程序本地化


Windows 8 提供了支持的打印机扩展和 UWP 的设备应用程序开发的标准的、 已本地化的显示字符串。

通过新提供了这些标准的、 已本地化的显示字符串[ **IPrintSchemaCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/hh451256)对象以支持某些功能和其关联的标准选项。 下表显示了 Windows 8 可以使用其标准本地化的功能显示字符串：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>标准选项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>输入的箱</td>
<td>Job/Document/PageInputBin</td>
</tr>
<tr class="even">
<td>媒体类型</td>
<td>PageMediaType</td>
</tr>
<tr class="odd">
<td>双面打印</td>
<td>JobDuplexAllDocumentsContiguously</td>
</tr>
<tr class="even">
<td>排序规则</td>
<td>DocumentCollate</td>
</tr>
<tr class="odd">
<td>输出颜色</td>
<td>PageOutputColor</td>
</tr>
<tr class="even">
<td>Orientation</td>
<td>PageOrientation</td>
</tr>
<tr class="odd">
<td>每张多</td>
<td>JobNUpAllDocumentsContiguously</td>
</tr>
<tr class="even">
<td>打孔</td>
<td><ul>
<li><p>JobHolePunch</p></li>
<li><p>DocumentHolePunch</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>装订</td>
<td><ul>
<li><p>JobStapleAllDocuments</p></li>
<li><p>DocumentStaple</p></li>
</ul></td>
</tr>
<tr class="even">
<td>绑定</td>
<td><ul>
<li><p>JobBindAllDocuments</p></li>
<li><p>DocumentBinding</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>输出质量</td>
<td>PageOutputQuality</td>
</tr>
<tr class="even">
<td>媒体大小</td>
<td>PageMediaSize</td>
</tr>
</tbody>
</table>

 

此外，这些字符串是 PrintCapabilities，XML 形式提供，前提是该驱动程序未指定资源 DLL 使用的功能或选项的显示名称。 如果驱动程序未指定使用的资源 DLL 的显示名称，将在 XML 中，以及对旧 COMPSTUI 基于打印首选项用户界面使用以前版本的 Windows 提供。

跨不同的用户界面和 Api，显示名称各不相同。 使用以下三个流程图看到预期的本地化行为针对给定方案的概述。

下面的流程图 UWP 应用中显示的预期的本地化行为如下所示[ **IPrintSchemaFeature** ](https://msdn.microsoft.com/library/windows/hardware/hh451284)并[ **IPrintSchemaOption**](https://msdn.microsoft.com/library/windows/hardware/hh451335)系列的对象。

![Windows 应用、 iprintschemafeature 或 iprintschemaoption 本地化行为流程图](images/locstringmodern.png)

下列流程图显示了中的预期的本地化行为**PrintCapabilities** XML 文档。

![printcapabilities xml 文档的本地化行为流程图](images/locstringpcap.png)

下列流程图显示了标准、 基于 Compstui 的打印首选项对话框中的预期的本地化行为。

![本地化的 compstui 基于对话框的行为流程图 ](images/locstringcomp.png)

若要使用的 Microsoft 本地化显示名称，请按照此表中的说明正确编辑 GPD 或 PPD 配置文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>文件类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPD</td>
<td><ul>
<li><p>指定<strong><em>名称</strong>GPD 功能或选项的条目。</p></li>
<li><p>未指定 <strong></em>rcNameID</strong>条目。</p></li>
<li>对于以下功能/选项，还必须指定<strong> <em>PrintSchemaKeywordMap</strong>将 GPD 功能或选项映射到相应的打印架构定义的功能或选项，除非被指定为<a href="standard-features.md" data-raw-source="[Standard Features](standard-features.md)">标准功能</a>。 若要查看示例演示如何使用 <strong></em>PrintSchemaKeywordMap</strong>若要将功能映射，请参阅<a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">基于 GPD/PPD 的功能说明更改</a>。
o JobHolePunch，DocumentHolePunch o JobStapleAllDocuments DocumentStaple o JobBindAllDocuments，DocumentBinding o PageOutputQuality o PageMediaType</li>
<li><p>不使用为每张<strong> <em>PrintSchemaKeywordMap</strong>选项值。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>PPD</td>
<td><ul>
<li><p>使用 <strong></em>PrintSchemaKeywordMap</strong> PPD 功能或选项映射到相应的打印架构定义的功能或选项。 若要查看示例演示如何使用<strong> <em>PrintSchemaKeywordMap</strong>若要将功能映射，请参阅<a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">基于 GPD/PPD 的功能说明更改</a>。</p></li>
<li><p>不使用为每张 <strong></em>PrintSchemaKeywordMap</strong>选项值。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**本地化 PPD 基于驱动程序**

基于 PPD 驱动程序不支持资源 Dll。 因此，它可能有必要提供多个 PPD 文件。 Microsoft 建议使用 PPD 配置文件的 v4 打印驱动程序应使用本主题中介绍的方法包括每个区域设置的一个 PPD 文件。

## <a name="related-topics"></a>相关主题
[**IPrintSchemaCapabilities**](https://msdn.microsoft.com/library/windows/hardware/hh451256)  
[**IPrintSchemaFeature**](https://msdn.microsoft.com/library/windows/hardware/hh451284)  
[**IPrintSchemaOption**](https://msdn.microsoft.com/library/windows/hardware/hh451335)  
[基于 GPD/PPD 的功能说明更改](gpd-ppd-based-feature-description-changes.md)  
[标准功能](standard-features.md)  



