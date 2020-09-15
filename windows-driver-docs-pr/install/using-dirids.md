---
title: 使用 Dirids
description: 使用 Dirids
ms.assetid: 231bc313-b5c3-48ef-b2e2-c4e287517679
keywords:
- dirids WDK
- INF 文件 WDK 设备安装，目录标识符
- 目录标识符 WDK INF 文件
- 目录 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 118f1adcce90022fc1aef71f55dc3cd28c5fbd07
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104088"
---
# <a name="using-dirids"></a>使用 Dirids





INF 文件中的许多目录都可以通过使用目录标识符 (*dirids*) 来表示，该标识符是标识特定目录的数字。 应用程序可以使用，但不能重新分配与 *dirids* 关联的系统定义目录，其值介于-1 到32767之间。

若要使用32768到65534、65536及更高的值创建 *dirids* ，请使用 Microsoft Windows SDK 文档) 中所述的 **SetupSetDirectoryId** (函数。

请注意，值为65535的 *dirid* 被视为具有值为-1 的 *dirid* 的同义词，不过，后者 (*dirid* -1) 是首选的。

如果要在 INF 文件中使用 *dirids* ，请考虑以下两个准则：

1. 当 INF 文件条目的语法明确指定 *dirid* 值 ([**INF DestinationDirs 部分**](inf-destinationdirs-section.md)时（例如) ，将该值表示为数字）。

   下面的示例演示了此语法：

   ```cpp
   [DestinationDirs]
   DefaultDestDir = 11  ;  \system32 directory on Windows 2000 and later versions
   ```

2. 当 INF 文件条目的语法指定文件路径时，可以使用系统提供的字符串替换来表示此路径的部分或全部。 此替换形式的格式如下：

   **%**<em>dirid</em>**%**

   此窗体包含百分号 (% ) 字符，后跟要指定的目录的 *dirid* ，后跟另一个百分比 (% ) 字符。 终止的反斜杠 (\) 字符将此表达式与路径中的以下文件名或其他目录隔开<strong>。</strong>

   下面的示例演示了此语法：

   ```cpp
   [aic78xx_Service_Inst]
   ServiceBinary = %12%\aic78xx.sys
   ```

   完全展开后，在前面的示例中显示的路径将变成*c：* \\ *windows* \\ *system32* \\ *驱动程序* \\ *aic78xx.sys* (假定 windows 安装在*c：* \\ *windows*目录) 中。 请注意，字符串替换或%*dirid*% 格式可以在预期字符串的任何位置使用，但 inf 文件的 [**inf 字符串部分**](inf-strings-section.md) 除外。

   下面两个示例演示如何使用字符串替换*not* 。

   ```cpp
   [DestinationDirs]
   DefaultDestDir = %11%  ; Error! - number expected

   [aic78xx_Service_Inst]
   ServiceBinary = 12\aic78xx.sys  ; Error! - unknown directory name
   ```

   在第一个示例中， **DefaultDestDir** 项的语法要求其值为数值。 但是，%11% 表达式扩展为字符串。 在第二个示例中，INF 编写器显然打算将 **ServiceBinary** 条目的值设置为包含驱动程序的目录中的文件 (参阅下表以了解详细信息) 。 之所以发生此错误，是因为 Windows 将在名为 "12" 的目录中查找指定文件，这可能在计算机上不存在。

下表显示了几个常用的 *dirids*及其表示的目录。 设备 INF 文件和驱动程序 INF 文件最常指定的值在表的顶部列出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">目标目录</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>2001</strong></p></td>
<td align="left"><p><em>SourceDrive</em><strong>： \</strong><em>pathname</em> (用于安装 INF 文件的目录) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>10</strong></p></td>
<td align="left"><p>Windows 目录。</p>
<p>这等同于 <em>% SystemRoot%</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>11</strong></p></td>
<td align="left"><p>系统目录。</p>
<p>这等效于<em>%SystemRoot%</em> <strong>\</strong> windows 2000 和更高版本的 windows 的% SystemRoot%<em>system32</em> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>12</strong></p></td>
<td align="left"><p>驱动程序目录。</p>
<p>这等效于<em>%SystemRoot%</em> <strong>\</strong> <em>system32</em> <strong>\</strong> windows 2000 和更高版本的 windows 的% SystemRoot% system32<em>驱动程序</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>13</strong></p></td>
<td align="left"><p>驱动程序包的 <a href="/windows-hardware/drivers/install/driver-store">驱动程序存储</a> 目录。</p>
<p>对于 Windows 8.1 及更高版本的 Windows，指定导入驱动程序包的驱动程序存储目录的路径。

请勿在<strong>DestinationDirs</strong>包括<em>dirid</em> 13 的文件上使用<a href="inf-delfiles-directive.md" data-raw-source="[DelFiles](inf-delfiles-directive.md)">DelFiles</a> 。

对于应用到此文件的条目，文件的 <strong>SourceDiskFiles</strong> 节中的可选子目录必须与 <strong>DestinationDirs</strong> 节中的子目录匹配。

不要使用 <a href="inf-copyfiles-directive.md" data-raw-source="[CopyFiles](inf-copyfiles-directive.md)">CopyFiles</a> 重命名 <strong>DestinationDirs</strong> 包括 <em>dirid</em> 13 的文件。
</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>17</strong></p></td>
<td align="left"><p>INF 文件目录</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>18</strong></p></td>
<td align="left"><p>帮助目录</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>20</strong></p></td>
<td align="left"><p>字体目录</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>21</strong></p></td>
<td align="left"><p>查看器目录</p></td>
</tr>
<tr class="even">
<td align="left"><p>23 </p></td>
<td align="left"><p>颜色目录 (ICM)  (<em>不</em> 用于安装打印机驱动程序) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>随时</strong></p></td>
<td align="left"><p>系统磁盘的根目录。</p>
<p>这是安装了 Windows 文件的磁盘的根目录。 例如，如果 <em>dirid</em> 10 是 "<em>C:\winnt</em>"，则 <em>dirid</em> 24 为 "<em>C：\</em>"。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>25</strong></p></td>
<td align="left"><p>共享目录</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>30</strong></p></td>
<td align="left"><p>启动磁盘（也称为 "ARC 系统分区"）的根目录。  (这与 <em>dirid</em> 24 ) 所表示的目录可能相同，也可能不相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>50</strong></p></td>
<td align="left"><p>系统目录</p>
<p>这等同于<em>% SystemRoot%</em> <strong>\</strong> <em>系统</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>51</strong></p></td>
<td align="left"><p>假脱机目录 (<em>不</em> 用于安装打印机驱动程序−请参阅 <a href="/windows-hardware/drivers/print/printer-dirids">printer Dirids</a>) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>52</strong></p></td>
<td align="left"><p>后台处理驱动程序目录 (<em>不</em> 用于安装打印机驱动程序) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>53</strong></p></td>
<td align="left"><p>用户配置文件目录</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>54</strong></p></td>
<td align="left"><p><em>Ntldr.exe</em>和<em>Osloader.exe</em>所在的目录</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>55</strong></p></td>
<td align="left"><p>打印处理器目录 (<em>不</em> 用于安装打印机驱动程序) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-1</strong></p></td>
<td align="left"><p>绝对路径</p></td>
</tr>
</tbody>
</table>

 

从16384到32767的*Dirid*值保留给特殊 shell 文件夹。 下表显示了这些文件夹的 *dirid* 值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">Shell 特殊文件夹</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>16406</strong></p></td>
<td align="left"><p><em>所有 Settings\all users\start 菜单</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16407</strong></p></td>
<td align="left"><p><em>所有 Settings\all users\start Menu\Programs</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16408</strong></p></td>
<td align="left"><p><em>所有 Settings\all users\start Menu\Programs\Startup</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16409</strong></p></td>
<td align="left"><p><em>所有 Users\Desktop</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16415</strong></p></td>
<td align="left"><p><em>所有 Users\Favorites</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16419</strong></p></td>
<td align="left"><p><em>所有 Users\Application 数据</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16422</strong></p></td>
<td align="left"><p><em>程序文件</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16425</strong></p></td>
<td align="left"><p><em>%SystemRoot%\SysWOW64</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16426</strong></p></td>
<td align="left"><p><em>%ProgramFiles(x86)%</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16427</strong></p></td>
<td align="left"><p><em>程序 Files\Common</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16428</strong></p></td>
<td align="left"><p><em>% ProgramFiles (x86) % \ Common</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16429</strong></p></td>
<td align="left"><p><em>所有 Users\Templates</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16430</strong></p></td>
<td align="left"><p><em>所有 Users\Documents</em></p></td>
</tr>
</tbody>
</table>

 

除了在*setupapi.log*中定义的此表中的值之外，还可以使用*Shlobj*中定义的任何 CSIDL_*Xxx*值。 若要为未在此表中列出的文件夹定义 *dirid* 值，请将 16384 (0x4000) 添加到 CSIDL_*Xxx* 值。 有关 CSIDL_*Xxx* 值的详细信息，请参阅 Windows SDK 文档。

 

