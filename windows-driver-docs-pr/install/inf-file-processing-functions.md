---
title: INF 文件处理函数
description: INF 文件处理函数
ms.assetid: df769d05-9843-44d2-971d-13f1a81755c2
keywords:
- Setupapi.log 函数 WDK，INF 文件
- INF 文件 WDK Setupapi.log
- SetupCopyOEMInf
- INF 文件处理函数 WDK Setupapi.log
- 处理函数 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b643b228966f4cae934058b826aa83138cc638ab
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105140"
---
# <a name="inf-file-processing-functions"></a>INF 文件处理函数





INF 文件处理函数提供了如下所示的设置和安装功能：

-   打开和关闭 INF 文件。

-   检索有关 INF 文件的信息。

-   检索有关复制操作的源文件和目标目录的信息。

-   执行 INF 文件部分中指定的安装操作。

下表列出了用于处理 INF 文件的函数。 有关详细的函数说明，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-installhinfsectiona" data-raw-source="[&lt;strong&gt;InstallHinfSection&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-installhinfsectiona)"><strong>InstallHinfSection</strong></a></p></td>
<td align="left"><p>执行指定 INF 文件中的指定节。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupcloseinffile" data-raw-source="[&lt;strong&gt;SetupCloseInfFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupcloseinffile)"><strong>SetupCloseInfFile</strong></a></p></td>
<td align="left"><p>释放资源并关闭 INF 句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupcopyoeminfa" data-raw-source="[&lt;strong&gt;SetupCopyOEMInf&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupcopyoeminfa)"><strong>SetupCopyOEMInf</strong></a></p></td>
<td align="left"><p>将文件复制到 <em>%SystemRoot%\Inf</em>中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdecompressorcopyfilea" data-raw-source="[&lt;strong&gt;SetupDecompressOrCopyFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdecompressorcopyfilea)"><strong>SetupDecompressOrCopyFile</strong></a></p></td>
<td align="left"><p>复制文件，并在必要时对其进行解压缩。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupfindfirstlinea" data-raw-source="[&lt;strong&gt;SetupFindFirstLine&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupfindfirstlinea)"><strong>SetupFindFirstLine</strong></a></p></td>
<td align="left"><p>查找指向 INF 文件的部分中第一行的指针，或者，如果指定了某个键，则查找与该键匹配的第一行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupfindnextline" data-raw-source="[&lt;strong&gt;SetupFindNextLine&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupfindnextline)"><strong>SetupFindNextLine</strong></a></p></td>
<td align="left"><p>返回指向 INF 文件部分中的下一行的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupfindnextmatchlinea" data-raw-source="[&lt;strong&gt;SetupFindNextMatchLine&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupfindnextmatchlinea)"><strong>SetupFindNextMatchLine</strong></a></p></td>
<td align="left"><p>返回指向 INF 文件部分中下一行的指针，或者，如果指定了某个键，则返回与该键匹配的下一行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetbinaryfield" data-raw-source="[&lt;strong&gt;SetupGetBinaryField&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetbinaryfield)"><strong>SetupGetBinaryField</strong></a></p></td>
<td align="left"><p>从 INF 文件中指定行中的字段检索二进制数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetfieldcount" data-raw-source="[&lt;strong&gt;SetupGetFieldCount&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetfieldcount)"><strong>SetupGetFieldCount</strong></a></p></td>
<td align="left"><p>返回行中的字段数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetfilecompressioninfoa" data-raw-source="[&lt;strong&gt;SetupGetFileCompressionInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetfilecompressioninfoa)"><strong>SetupGetFileCompressionInfo</strong></a></p></td>
<td align="left"><p>从 INF 文件中检索文件压缩信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetinfdriverstorelocationa" data-raw-source="[&lt;strong&gt;SetupGetInfDriverStoreLocation&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetinfdriverstorelocationa)"><strong>SetupGetInfDriverStoreLocation</strong></a></p></td>
<td align="left"><p>检索 <a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">驱动程序存储区</a> 中与系统 inf 文件目录中的指定 inf 文件或驱动程序存储区中的指定 inf 文件相对应的 (的目录路径和文件名) 的完全限定文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetinffilelista" data-raw-source="[&lt;strong&gt;SetupGetInfFileList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetinffilelista)"><strong>SetupGetInfFileList</strong></a></p></td>
<td align="left"><p>返回指定目录中的 INF 文件的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetinfinformationa" data-raw-source="[&lt;strong&gt;SetupGetInfInformation&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetinfinformationa)"><strong>SetupGetInfInformation</strong></a></p></td>
<td align="left"><p>返回有关 INF 文件的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetintfield" data-raw-source="[&lt;strong&gt;SetupGetIntField&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetintfield)"><strong>SetupGetIntField</strong></a></p></td>
<td align="left"><p>获取 INF 文件中指定行内指定字段的整数值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetinfpublishednamea" data-raw-source="[&lt;strong&gt;SetupGetInfPublishedName&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetinfpublishednamea)"><strong>SetupGetInfPublishedName</strong></a></p></td>
<td align="left"><p>检索系统 INF 文件目录中与系统 INF 文件目录中的指定 INF 文件或 <a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">驱动程序存储区</a>中指定 inf 文件相对应的 inf 文件 (目录路径和文件名) 的完全限定名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetlinebyindexa" data-raw-source="[&lt;strong&gt;SetupGetLineByIndex&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetlinebyindexa)"><strong>SetupGetLineByIndex</strong></a></p></td>
<td align="left"><p>返回一个指针，该指针指向与指定节中的指定索引值相关联的行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetlinecounta" data-raw-source="[&lt;strong&gt;SetupGetLineCount&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetlinecounta)"><strong>SetupGetLineCount</strong></a></p></td>
<td align="left"><p>返回指定节中的行数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetlinetexta" data-raw-source="[&lt;strong&gt;SetupGetLineText&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetlinetexta)"><strong>SetupGetLineText</strong></a></p></td>
<td align="left"><p>从 INF 文件中检索指定行的内容。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetmultiszfielda" data-raw-source="[&lt;strong&gt;SetupGetMultiSzField&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetmultiszfielda)"><strong>SetupGetMultiSzField</strong></a></p></td>
<td align="left"><p>返回多个字符串，从行中的指定字段开始。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetsourcefilelocationa" data-raw-source="[&lt;strong&gt;SetupGetSourceFileLocation&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetsourcefilelocationa)"><strong>SetupGetSourceFileLocation</strong></a></p></td>
<td align="left"><p>返回 INF 文件中列出的源文件的位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetsourcefilesizea" data-raw-source="[&lt;strong&gt;SetupGetSourceFileSize&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetsourcefilesizea)"><strong>SetupGetSourceFileSize</strong></a></p></td>
<td align="left"><p>返回在 INF 文件的指定节中列出的指定文件或一组文件的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetsourceinfoa" data-raw-source="[&lt;strong&gt;SetupGetSourceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetsourceinfoa)"><strong>SetupGetSourceInfo</strong></a></p></td>
<td align="left"><p>检索源的路径、标记文件或说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetstringfielda" data-raw-source="[&lt;strong&gt;SetupGetStringField&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetstringfielda)"><strong>SetupGetStringField</strong></a></p></td>
<td align="left"><p>从 INF 文件中指定行中的字段检索字符串数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgettargetpatha" data-raw-source="[&lt;strong&gt;SetupGetTargetPath&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgettargetpatha)"><strong>SetupGetTargetPath</strong></a></p></td>
<td align="left"><p>确定指定 INF 文件部分中列出的文件的目标路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupinstallfilea" data-raw-source="[&lt;strong&gt;SetupInstallFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupinstallfilea)"><strong>SetupInstallFile</strong></a></p></td>
<td align="left"><p>将指定文件安装到特定目标目录中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupinstallfileexa" data-raw-source="[&lt;strong&gt;SetupInstallFileEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupinstallfileexa)"><strong>SetupInstallFileEx</strong></a></p></td>
<td align="left"><p>将指定文件安装到特定目标目录中。 如果正在使用该文件的现有版本，则安装将会延迟。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupinstallfilesfrominfsectiona" data-raw-source="[&lt;strong&gt;SetupInstallFilesFromInfSection&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupinstallfilesfrominfsectiona)"><strong>SetupInstallFilesFromInfSection</strong></a></p></td>
<td align="left"><p>对指定 INF 文件部分中的文件进行排队以进行复制。  (与 <a href="/windows/desktop/api/setupapi/nf-setupapi-setupqueuecopysectiona" data-raw-source="[&lt;strong&gt;SetupQueueCopySection&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupqueuecopysectiona)"><strong>SetupQueueCopySection</strong></a>相同 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupinstallfrominfsectiona" data-raw-source="[&lt;strong&gt;SetupInstallFromInfSection&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupinstallfrominfsectiona)"><strong>SetupInstallFromInfSection</strong></a></p></td>
<td align="left"><p>执行 INF <em>DDInstall</em> 部分中指定的指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupinstallservicesfrominfsectiona" data-raw-source="[&lt;strong&gt;SetupInstallServicesFromInfSection&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupinstallservicesfrominfsectiona)"><strong>SetupInstallServicesFromInfSection</strong></a></p></td>
<td align="left"><p>执行 INF DDInstall 中指定的服务安装和删除操作<em>DDInstall</em><strong>。服务</strong>部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupopenappendinffilea" data-raw-source="[&lt;strong&gt;SetupOpenAppendInfFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupopenappendinffilea)"><strong>SetupOpenAppendInfFile</strong></a></p></td>
<td align="left"><p>打开一个 INF 文件，并将其追加到现有 INF 句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupopeninffilea" data-raw-source="[&lt;strong&gt;SetupOpenInfFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupopeninffilea)"><strong>SetupOpenInfFile</strong></a></p></td>
<td align="left"><p>打开一个 INF 文件并返回该文件的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupopenmasterinf" data-raw-source="[&lt;strong&gt;SetupOpenMasterInf&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupopenmasterinf)"><strong>SetupOpenMasterInf</strong></a></p></td>
<td align="left"><p>打开主 INF 文件，其中包含操作系统默认安装中所包含文件的文件和布局信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupqueryinffileinformationa" data-raw-source="[&lt;strong&gt;SetupQueryInfFileInformation&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupqueryinffileinformationa)"><strong>SetupQueryInfFileInformation</strong></a></p></td>
<td align="left"><p>返回指定 INF 文件的一个构成 INF 文件的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupqueryinfversioninformationa" data-raw-source="[&lt;strong&gt;SetupQueryInfVersionInformation&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupqueryinfversioninformationa)"><strong>SetupQueryInfVersionInformation</strong></a></p></td>
<td align="left"><p>返回指定 INF 文件的其中一个 INF 文件的版本号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupsetdirectoryida" data-raw-source="[&lt;strong&gt;SetupSetDirectoryId&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupsetdirectoryida)"><strong>SetupSetDirectoryId</strong></a></p></td>
<td align="left"><p>将)  (DIRID 的目录 ID 分配到指定的目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupuninstalloeminfa" data-raw-source="[&lt;strong&gt;SetupUninstallOEMInf&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupuninstalloeminfa)"><strong>SetupUninstallOEMInf</strong></a></p></td>
<td align="left"><p>卸载指定的 INF 文件，并删除关联的。<em>pnf</em> 和。<em>cat</em> 文件（如果存在）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupverifyinffilea" data-raw-source="[&lt;strong&gt;SetupVerifyInfFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupverifyinffilea)"><strong>SetupVerifyInfFile</strong></a></p></td>
<td align="left"><p>验证是否未修改经过数字签名的 INF 文件。  (Windows XP 和更高版本。 ) </p></td>
</tr>
</tbody>
</table>

 

