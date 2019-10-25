---
title: V4 打印机驱动程序本地化
description: Windows 8 提供了标准的本地化显示字符串，以支持打印机扩展和 UWP 设备应用程序的开发。
ms.assetid: 5C587AF2-C51E-4728-A214-7FC1F8A6E445
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d4d5c24d481953c0e07ddc209d2986cf5a5117
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844196"
---
# <a name="v4-printer-driver-localization"></a>V4 打印机驱动程序本地化


Windows 8 提供了标准的本地化显示字符串，以支持打印机扩展和 UWP 设备应用程序的开发。

这些标准的本地化显示字符串通过新的[**IPrintSchemaCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)对象提供，用于支持某些功能及其关联的标准选项。 下表显示了 Windows 8 可以用其标准显示字符串本地化的功能：

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
<td>输入纸盒</td>
<td>作业/文档/PageInputBin</td>
</tr>
<tr class="even">
<td>媒体类型</td>
<td>PageMediaType</td>
</tr>
<tr class="odd">
<td>打印</td>
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
<td>N 向上</td>
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

 

此外，这些字符串在 PrintCapabilities 的 XML 格式中提供，前提是该驱动程序不使用该功能或选项的资源 DLL 指定显示名称。 如果驱动程序使用资源 DLL 指定显示名称，它将在 XML 中提供，并在以前版本的 Windows 上使用的基于旧版 COMPSTUI 打印首选项 UI。

在不同的用户界面和 Api 上，显示名称有所不同。 使用以下三个流程图查看给定方案的预期本地化行为的概述。

以下流程图显示了 UWP 应用中的预期本地化行为以及对象的[**IPrintSchemaFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemafeature)和[**IPrintSchemaOption**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemaoption)系列。

![适用于 Windows apps、iprintschemafeature 或 iprintschemaoption 的本地化行为流程图](images/locstringmodern.png)

以下流程图显示了**PrintCapabilities** XML 文档中的预期本地化行为。

![printcapabilities xml 文档的本地化行为流程图](images/locstringpcap.png)

以下流程图显示了标准的、基于 Compstui 的打印首选项对话框中的预期本地化行为。

![基于 compstui 的对话框的本地化行为流程图 ](images/locstringcomp.png)

若要使用 Microsoft 本地化的显示名称，请按照此表中的说明进行操作，以正确编辑 GPD 或 PPD 配置文件。

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
<li><p>为 GPD 功能或选项指定 <strong><em>名称</strong> 条目。</p></li>
<li><p>不要指定<strong></em>rcNameID</strong> "项。</p></li>
<li>对于以下功能/选项，还必须指定 <strong><em>PrintSchemaKeywordMap</strong> 将 GPD 功能或选项映射到相应的打印架构定义的功能或选项，除非将它们指定为<a href="standard-features.md" data-raw-source="[Standard Features](standard-features.md)">标准功能</a>. 若要查看演示如何使用<strong></em>PrintSchemaKeywordMap</strong>映射功能的示例，请参阅<a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">GPD/基于 PPD 的功能说明更改</a>。
o JobHolePunch，DocumentHolePunch o JobStapleAllDocuments，DocumentStaple o JobBindAllDocuments，DocumentBinding o PageOutputQuality o PageMediaType</li>
<li><p>对于 "N 向上"，请不要在选项值上使用 <strong><em>PrintSchemaKeywordMap</strong>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>信息库</td>
<td><ul>
<li><p>使用<strong></em>PrintSchemaKeywordMap</strong>将 PPD 功能或选项映射到相应的打印架构定义的功能或选项。 若要查看演示如何使用 <strong><em>PrintSchemaKeywordMap</strong> 映射功能的示例，请参阅<a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">GPD/基于 PPD 的功能说明更改</a>。</p></li>
<li><p>对于 "N 向上"，请不要对选项值使用<strong></em>PrintSchemaKeywordMap</strong> 。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**本地化基于 PPD 的驱动程序**

基于 PPD 的驱动程序不支持资源 Dll。 因此，可能需要提供多个 PPD 文件。 Microsoft 建议使用 PPD 配置文件的 v4 打印驱动程序应使用本主题中所述的方法在每个区域设置中包含一个 PPD 文件。

## <a name="related-topics"></a>相关主题
[**IPrintSchemaCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)  
[**IPrintSchemaFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemafeature)  
[**IPrintSchemaOption**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemaoption)  
[基于 GPD/PPD 的功能说明更改](gpd-ppd-based-feature-description-changes.md)  
[标准功能](standard-features.md)  



