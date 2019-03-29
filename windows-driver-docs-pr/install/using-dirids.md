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
ms.openlocfilehash: e977273eaca5dc17251a24b73451bce303047e5d
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463853"
---
# <a name="using-dirids"></a>使用 Dirids





可以通过使用目录标识符表示许多会显示在 INF 文件的目录 (*dirids*)，这是标识特定的目录的数字。 应用程序可以使用，但不能重新分配与关联的系统定义的目录*dirids*其值是从-1 到 32767 之间。

若要创建*dirids* 32768 通过 65534 或 65536 和更高，使用从用户定义的值与**SetupSetDirectoryId**函数 （Microsoft Windows SDK 文档中所述）。

请注意， *dirid*值为 65535 被视为与*dirid*值为-1，尽管后者 (*dirid* -1) 是首选。

如果你想要使用*dirids*在 INF 文件中，请考虑以下两个指导原则：

1. INF 文件条目的语法显式指定*dirid*值 ( [ **INF DestinationDirs 部分**](inf-destinationdirs-section.md)，例如)，表示为数字的值。

   下面的示例演示了此语法：

   ```cpp
   [DestinationDirs]
   DefaultDestDir = 11  ;  \system32 directory on Windows 2000 and later versions
   ```

2. 当一个 INF 文件条目的语法指定文件路径时，可以使用系统提供的字符串替换来表示部分或全部此路径。 这种替换具有以下形式：

   **%**<em>dirid</em>**%**

   此窗体包含百分号 （%）字符后, 跟*dirid*你想要指定的目录后, 跟另一个百分号 （%）字符。 终止反斜杠 (\)字符将此表达式与以下文件名称或其他目录路径中的分隔开来<strong>。</strong>

   下面的示例演示了此语法：

   ```cpp
   [aic78xx_Service_Inst]
   ServiceBinary = %12%\aic78xx.sys
   ```

   当完全展开，在前面的示例所示的路径将成为*c:*\\*windows*\\*system32* \\ *驱动程序*\\*aic78xx.sys* (假设 Windows 是否已安装在*c:*\\*windows*目录）。 请注意，字符串替换或 %*dirid*%窗体中，可以使用任何位置应有一个字符串，除[ **INF 字符串部分**](inf-strings-section.md)的 INF 文件。

   两个以下示例演示如何替换字符串应*不*使用。

   ```cpp
   [DestinationDirs]
   DefaultDestDir = %11%  ; Error! - number expected

   [aic78xx_Service_Inst]
   ServiceBinary = 12\aic78xx.sys  ; Error! - unknown directory name
   ```

   在第一个示例中的语法**DefaultDestDir**项需要其值应为数字。 但是，%11%表达式扩展到字符串。 在第二个示例中，INF 编写器显然用于设置的值**ServiceBinary**进入包含驱动程序 （请参阅下表中的详细信息） 的目录中的文件。 出错的原因在于 Windows 将查找名为"12"可能不存在的计算机上的目录中的指定文件。

下表显示了几种常用*dirids*，以及它们所代表的目录。 表在顶部列出了最常由设备 INF 文件和驱动程序 INF 文件指定的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">目标目录</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>01</strong></p></td>
<td align="left"><p><em>SourceDrive</em><strong>: \</strong><em>路径名</em>（从其 INF 文件已安装的目录）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>10</strong></p></td>
<td align="left"><p>Windows 目录。</p>
<p>这相当于<em>%systemroot%</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>11</strong></p></td>
<td align="left"><p>系统目录。</p>
<p>这相当于<em>%systemroot%</em><strong>\</strong><em>system32</em>对于 Windows 2000 和更高版本的 Windows...</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>12</strong></p></td>
<td align="left"><p>驱动程序目录。</p>
<p>这相当于<em>%systemroot%</em><strong>\</strong><em>system32</em><strong>\</strong><em>的驱动程序</em> Windows 2000 和更高版本的 Windows。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>13</strong></p></td>
<td align="left"><p>驱动程序包<a href="https://msdn.microsoft.com/windows/hardware/drivers/install/driver-store">驱动程序存储区</a>目录。</p>
<p>对于 Windows 8.1 和更高版本的 Windows，指定驱动程序包已导入其中的驱动程序存储区目录的路径。

不要使用<a href="inf-delfiles-directive.md" data-raw-source="[DelFiles](inf-delfiles-directive.md)">DelFiles</a>上的文件<strong>DestinationDirs</strong>包括<em>dirid</em> 13。

中的可选子目录<strong>SourceDiskFiles</strong>部分的文件必须与匹配的子目录中<strong>DestinationDirs</strong>部分，了解适用于此文件的条目。

不要使用<a href="inf-copyfiles-directive.md" data-raw-source="[CopyFiles](inf-copyfiles-directive.md)">CopyFiles</a>若要为其重命名文件<strong>DestinationDirs</strong>包括<em>dirid</em> 13。
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
<td align="left"><p><strong>23</strong></p></td>
<td align="left"><p>颜色目录 (ICM) (<em>不</em>用于安装打印机驱动程序)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>24</strong></p></td>
<td align="left"><p>系统磁盘的根目录。</p>
<p>这是磁盘的在其安装 Windows 文件的根目录。 例如，如果<em>dirid</em> 10 是"<em>C:\winnt</em>"，然后<em>dirid</em> 24 是"<em>C:\</em>"。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>25</strong></p></td>
<td align="left"><p>共享的目录</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>30</strong></p></td>
<td align="left"><p>启动磁盘，也称为"弧线系统分区"的根目录。 (这可能会也可能不是由表示一个与相同的目录<em>dirid</em> 24。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>50</strong></p></td>
<td align="left"><p>系统目录</p>
<p>这相当于<em>%systemroot%</em><strong>\</strong><em>系统</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>51</strong></p></td>
<td align="left"><p>假脱机目录 (<em>不</em>用于安装打印机驱动程序，请参阅 −<a href="https://msdn.microsoft.com/library/windows/hardware/ff560821">打印机 Dirids</a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>52</strong></p></td>
<td align="left"><p>后台打印驱动程序目录 (<em>不</em>用于安装打印机驱动程序)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>53</strong></p></td>
<td align="left"><p>用户配置文件目录</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>54</strong></p></td>
<td align="left"><p>目录位置<em>Ntldr.exe</em>并<em>Osloader.exe</em>所在</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>55</strong></p></td>
<td align="left"><p>打印处理器目录 (<em>不</em>用于安装打印机驱动程序)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-1</strong></p></td>
<td align="left"><p>绝对路径</p></td>
</tr>
</tbody>
</table>

 

*Dirid*对于特定的解释器文件夹保留从 16384 到 32767 之间的值。 下表显示*dirid*这些文件夹的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">Shell 特殊文件夹</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>16406</strong></p></td>
<td align="left"><p><em>所有 Users\Start 菜单</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16407</strong></p></td>
<td align="left"><p><em>所有 Users\Start Menu\Programs</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16408</strong></p></td>
<td align="left"><p><em>所有 Users\Start Menu\Programs\Startup</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16409</strong></p></td>
<td align="left"><p><em>All Users\Desktop</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16415</strong></p></td>
<td align="left"><p><em>All Users\Favorites</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16419</strong></p></td>
<td align="left"><p><em>所有用户 \ 应用程序数据</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16422</strong></p></td>
<td align="left"><p><em>程序文件</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16425</strong></p></td>
<td align="left"><p><em>%SystemRoot%\system32</em> （适用于 Windows (WOW64) 运行在 Windows 下的 Microsoft Win32 用户模式应用程序）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16426</strong></p></td>
<td align="left"><p><em>程序文件</em>（适用于 Win32 的 WOW64 下运行的用户模式应用程序）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16427</strong></p></td>
<td align="left"><p><em>Program Files\Common</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16428</strong></p></td>
<td align="left"><p><em>程序 Files\Common</em> （适用于 Win32 的 WOW64 下运行的用户模式应用程序）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16429</strong></p></td>
<td align="left"><p><em>所有 Users\Templates</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16430</strong></p></td>
<td align="left"><p><em>所有用户 \ 文件</em></p></td>
</tr>
</tbody>
</table>

 

除了中定义此表中的值*Setupapi.h*，可以使用任何 CSIDL_*Xxx*中定义的值*Shlobj.h*。 若要定义*dirid*值对此表未列出的某个文件夹时，请将 16384 (0x4000) 添加到 CSIDL_*Xxx*值。 详细了解 CSIDL_*Xxx*值，请参阅 Windows SDK 文档。

 

 





