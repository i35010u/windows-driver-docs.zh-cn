---
title: INF 文件处理函数
description: INF 文件处理函数
ms.assetid: df769d05-9843-44d2-971d-13f1a81755c2
keywords:
- 安装程序 Api 函数 WDK、 INF 文件
- INF 文件 WDK SetupAPI
- SetupCopyOEMInf
- INF 文件处理函数 WDK SetupAPI
- 处理函数 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b0f569074bd759cc377fdfe43528b098a674882
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391989"
---
# <a name="inf-file-processing-functions"></a>INF 文件处理函数





INF 文件处理函数提供了设置和安装功能，其中包括以下：

-   打开和关闭的 INF 文件。

-   检索一个 INF 文件有关的信息。

-   检索有关源文件和目标目录用于复制操作的信息。

-   执行 INF 文件节中指定的安装操作。

下表列出了用于处理 INF 文件的函数。 有关详细的功能描述，请参阅 Microsoft Windows SDK 文档。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376957" data-raw-source="[&lt;strong&gt;InstallHinfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376957)"><strong>InstallHinfSection</strong></a></p></td>
<td align="left"><p>执行指定的 INF 文件中指定的节。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376985" data-raw-source="[&lt;strong&gt;SetupCloseInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376985)"><strong>SetupCloseInfFile</strong></a></p></td>
<td align="left"><p>释放资源并关闭 INF 句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376990" data-raw-source="[&lt;strong&gt;SetupCopyOEMInf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376990)"><strong>SetupCopyOEMInf</strong></a></p></td>
<td align="left"><p>复制将文件放<em>%SystemRoot%\Inf</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376992" data-raw-source="[&lt;strong&gt;SetupDecompressOrCopyFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376992)"><strong>SetupDecompressOrCopyFile</strong></a></p></td>
<td align="left"><p>复制文件，并如有必要，会将其解压缩。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376996" data-raw-source="[&lt;strong&gt;SetupFindFirstLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376996)"><strong>SetupFindFirstLine</strong></a></p></td>
<td align="left"><p>INF 文件的部分中找到的第一行的指针; 如果指定了密钥，与键匹配的第一个行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376997" data-raw-source="[&lt;strong&gt;SetupFindNextLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376997)"><strong>SetupFindNextLine</strong></a></p></td>
<td align="left"><p>返回一个指向 INF 文件部分中的下一行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377202" data-raw-source="[&lt;strong&gt;SetupFindNextMatchLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377202)"><strong>SetupFindNextMatchLine</strong></a></p></td>
<td align="left"><p>返回一个指针到下一行中 INF 文件部分，或如果指定了密钥的下一个行的键相匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377254" data-raw-source="[&lt;strong&gt;SetupGetBinaryField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377254)"><strong>SetupGetBinaryField</strong></a></p></td>
<td align="left"><p>从 INF 文件中的指定行中的字段中检索二进制数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377258" data-raw-source="[&lt;strong&gt;SetupGetFieldCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377258)"><strong>SetupGetFieldCount</strong></a></p></td>
<td align="left"><p>在行中返回字段的数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377265" data-raw-source="[&lt;strong&gt;SetupGetFileCompressionInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377265)"><strong>SetupGetFileCompressionInfo</strong></a></p></td>
<td align="left"><p>从 INF 文件中检索文件压缩信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552194" data-raw-source="[&lt;strong&gt;SetupGetInfDriverStoreLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552194)"><strong>SetupGetInfDriverStoreLocation</strong></a></p></td>
<td align="left"><p>检索的 INF 文件中的完全限定的文件名 （目录路径和文件名）<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">驱动程序存储区</a>对应于系统 INF 文件目录中指定的 INF 文件或驱动程序存储区中的指定的 INF 文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377381" data-raw-source="[&lt;strong&gt;SetupGetInfFileList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377381)"><strong>SetupGetInfFileList</strong></a></p></td>
<td align="left"><p>返回指定目录中的 INF 文件列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377383" data-raw-source="[&lt;strong&gt;SetupGetInfInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377383)"><strong>SetupGetInfInformation</strong></a></p></td>
<td align="left"><p>返回一个 INF 文件有关的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377385" data-raw-source="[&lt;strong&gt;SetupGetIntField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377385)"><strong>SetupGetIntField</strong></a></p></td>
<td align="left"><p>获取一个 INF 文件中的指定行中的指定字段的整数值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552200" data-raw-source="[&lt;strong&gt;SetupGetInfPublishedName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552200)"><strong>SetupGetInfPublishedName</strong></a></p></td>
<td align="left"><p>检索对应于系统 INF 文件目录中指定的 INF 文件或指定的 INF 文件中的系统 INF 文件目录中的 INF 文件的完全限定的名称 （目录路径和文件名）<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">驱动程序存储区</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377386" data-raw-source="[&lt;strong&gt;SetupGetLineByIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377386)"><strong>SetupGetLineByIndex</strong></a></p></td>
<td align="left"><p>返回一个指向与指定的节中的指定的索引值相关联的行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377387" data-raw-source="[&lt;strong&gt;SetupGetLineCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377387)"><strong>SetupGetLineCount</strong></a></p></td>
<td align="left"><p>指定的节中返回行的数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377388" data-raw-source="[&lt;strong&gt;SetupGetLineText&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377388)"><strong>SetupGetLineText</strong></a></p></td>
<td align="left"><p>从 INF 文件中检索指定行的内容。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377389" data-raw-source="[&lt;strong&gt;SetupGetMultiSzField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377389)"><strong>SetupGetMultiSzField</strong></a></p></td>
<td align="left"><p>返回多个字符串，开始的行中指定的字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377390" data-raw-source="[&lt;strong&gt;SetupGetSourceFileLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377390)"><strong>SetupGetSourceFileLocation</strong></a></p></td>
<td align="left"><p>返回 INF 文件中列出的源文件的位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377391" data-raw-source="[&lt;strong&gt;SetupGetSourceFileSize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377391)"><strong>SetupGetSourceFileSize</strong></a></p></td>
<td align="left"><p>返回指定文件的大小或一组在指定的节的 INF 文件中列出的文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377392" data-raw-source="[&lt;strong&gt;SetupGetSourceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377392)"><strong>SetupGetSourceInfo</strong></a></p></td>
<td align="left"><p>检索路径、 标记文件或源的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377393" data-raw-source="[&lt;strong&gt;SetupGetStringField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377393)"><strong>SetupGetStringField</strong></a></p></td>
<td align="left"><p>检索字符串数据从一个 INF 文件中的指定行中的字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377394" data-raw-source="[&lt;strong&gt;SetupGetTargetPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377394)"><strong>SetupGetTargetPath</strong></a></p></td>
<td align="left"><p>确定指定的 INF 文件部分中列出的文件的目标路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377398" data-raw-source="[&lt;strong&gt;SetupInstallFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377398)"><strong>SetupInstallFile</strong></a></p></td>
<td align="left"><p>将指定的文件安装到特定目标目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377399" data-raw-source="[&lt;strong&gt;SetupInstallFileEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377399)"><strong>SetupInstallFileEx</strong></a></p></td>
<td align="left"><p>将指定的文件安装到特定目标目录。 如果正在使用中的现有文件的版本，安装会延迟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377400" data-raw-source="[&lt;strong&gt;SetupInstallFilesFromInfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377400)"><strong>SetupInstallFilesFromInfSection</strong></a></p></td>
<td align="left"><p>队列中指定的 INF 文件的文件将复制的部分。 (与相同<a href="https://msdn.microsoft.com/library/windows/desktop/aa377423" data-raw-source="[&lt;strong&gt;SetupQueueCopySection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377423)"> <strong>SetupQueueCopySection</strong></a>。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377401" data-raw-source="[&lt;strong&gt;SetupInstallFromInfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377401)"><strong>SetupInstallFromInfSection</strong></a></p></td>
<td align="left"><p>执行 INF 中指定的指令<em>DDInstall</em>部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377402" data-raw-source="[&lt;strong&gt;SetupInstallServicesFromInfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377402)"><strong>SetupInstallServicesFromInfSection</strong></a></p></td>
<td align="left"><p>执行 INF 中指定的服务安装和删除操作<em>DDInstall</em><strong>。服务</strong>部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377407" data-raw-source="[&lt;strong&gt;SetupOpenAppendInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377407)"><strong>SetupOpenAppendInfFile</strong></a></p></td>
<td align="left"><p>打开一个 INF 文件并将其追加到现有 INF 句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377409" data-raw-source="[&lt;strong&gt;SetupOpenInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377409)"><strong>SetupOpenInfFile</strong></a></p></td>
<td align="left"><p>打开一个 INF 文件，并返回的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377411" data-raw-source="[&lt;strong&gt;SetupOpenMasterInf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377411)"><strong>SetupOpenMasterInf</strong></a></p></td>
<td align="left"><p>将打开包含已包含操作系统的默认安装的文件的文件和布局信息的主 INF 文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377416" data-raw-source="[&lt;strong&gt;SetupQueryInfFileInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377416)"><strong>SetupQueryInfFileInformation</strong></a></p></td>
<td align="left"><p>返回一个指定的 INF 文件的构成 INF 文件的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377418" data-raw-source="[&lt;strong&gt;SetupQueryInfVersionInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377418)"><strong>SetupQueryInfVersionInformation</strong></a></p></td>
<td align="left"><p>返回一个指定的 INF 文件的构成 INF 文件的版本号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377436" data-raw-source="[&lt;strong&gt;SetupSetDirectoryId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377436)"><strong>SetupSetDirectoryId</strong></a></p></td>
<td align="left"><p>将目录 ID (DIRID) 分配给指定的目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377446" data-raw-source="[&lt;strong&gt;SetupUninstallOEMInf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377446)"><strong>SetupUninstallOEMInf</strong></a></p></td>
<td align="left"><p>卸载指定的 INF 文件，并删除关联。<em>pnf</em>和。<em>cat</em>文件，如果它们存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377447" data-raw-source="[&lt;strong&gt;SetupVerifyInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377447)"><strong>SetupVerifyInfFile</strong></a></p></td>
<td align="left"><p>验证尚未修改已进行数字签名的 INF 文件。 (Windows XP 及更高版本。)</p></td>
</tr>
</tbody>
</table>

 

 

 





