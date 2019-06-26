---
title: 磁盘空间列表函数
description: 磁盘空间列表函数
ms.assetid: 850e9f41-b534-49f3-891d-c12c1126e52f
keywords:
- 列表的安装程序 Api 函数 WDK，磁盘空间
- 磁盘空间列出了 WDK SetupAPI
- 计算磁盘空间 WDK SetupAPI
- 空间计算 WDK SetupAPI
- 磁盘空间计算 WDK SetupAPI
- 总磁盘空间计算 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ada6fe327b1ac6c1e1c78dbdf3abe49e091bd88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375301"
---
# <a name="disk-space-list-functions"></a>磁盘空间列表函数





磁盘空间列表函数用于创建和修改磁盘空间列表。 这些列表可用于计算处理的文件将复制或删除在安装过程中所需的总磁盘空间。

下表列出了可用于操作磁盘空间列表的函数。 有关详细的功能描述，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddinstallsectiontodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddInstallSectionToDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddinstallsectiontodiskspacelista)"><strong>SetupAddInstallSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>搜索<strong>CopyFile</strong>并<strong>DelFile</strong>中的指令<em>DDInstall</em>部分的 INF 文件，然后将添加到磁盘空间列表的那些部分中指定的文件操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddsectiontodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddSectionToDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddsectiontodiskspacelista)"><strong>SetupAddSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>将添加到所有文件将都复制的磁盘空间列表或在指定的节的 INF 文件中列出的删除操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddtodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddToDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddtodiskspacelista)"><strong>SetupAddToDiskSpaceList</strong></a></p></td>
<td align="left"><p>将单个删除或复制操作添加到的磁盘空间列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcreatediskspacelista" data-raw-source="[&lt;strong&gt;SetupCreateDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcreatediskspacelista)"><strong>SetupCreateDiskSpaceList</strong></a></p></td>
<td align="left"><p>创建的磁盘空间列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdestroydiskspacelist" data-raw-source="[&lt;strong&gt;SetupDestroyDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdestroydiskspacelist)"><strong>SetupDestroyDiskSpaceList</strong></a></p></td>
<td align="left"><p>销毁磁盘空间列表并释放分配给它的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupquerydrivesindiskspacelista" data-raw-source="[&lt;strong&gt;SetupQueryDrivesInDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupquerydrivesindiskspacelista)"><strong>SetupQueryDrivesInDiskSpaceList</strong></a></p></td>
<td align="left"><p>引用的磁盘空间列表中列出的文件操作的驱动器的列表的填充调用方提供的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryspacerequiredondrivea" data-raw-source="[&lt;strong&gt;SetupQuerySpaceRequiredOnDrive&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryspacerequiredondrivea)"><strong>SetupQuerySpaceRequiredOnDrive</strong></a></p></td>
<td align="left"><p>检查磁盘空间列表，以确定特定驱动器的执行列出的所有文件操作所需的空间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefromdiskspacelista" data-raw-source="[&lt;strong&gt;SetupRemoveFromDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefromdiskspacelista)"><strong>SetupRemoveFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>删除文件复制或从磁盘空间列表中删除操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremoveinstallsectionfromdiskspacelista" data-raw-source="[&lt;strong&gt;SetupRemoveInstallSectionFromDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremoveinstallsectionfromdiskspacelista)"><strong>SetupRemoveInstallSectionFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>搜索<strong>CopyFiles</strong>并<strong>DelFiles</strong>中的指令<em>DDInstall</em>的 INF 文件，并删除文件操作从磁盘空间的那些部分中指定的部分列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetupRemoveSectionFromDiskSpaceList</strong></p></td>
<td align="left"><p>磁盘空间会列出文件复制或删除在指定的节的 INF 文件中列出的操作。</p></td>
</tr>
</tbody>
</table>

 

 

 





