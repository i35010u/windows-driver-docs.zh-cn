---
title: SymStore 事务
description: SymStore 事务
ms.assetid: f0bb2f3f-0f6b-4ed6-809e-f55b1c537d7f
keywords:
- SymStore 事务
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a4a657cd27e7a852210c6ae5f982e9f1e4390b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526438"
---
# <a name="symstore-transactions"></a>SymStore 事务


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore 的每个调用记录为一个事务。 有两种类型的事务： 添加和删除。

创建符号存储区时，服务器的根目录下创建一个名为"000admin"的目录。 000admin 目录包含一个文件的每个事务，以及日志文件 server.txt 和 history.txt。 Server.txt 文件包含目前在服务器的所有事务的列表。 History.txt 文件包含所有事务按时间历史的记录。

SymStore 存储或删除符号的文件，每次都会创建新的事务数。 然后，000admin 中创建一个文件，其名称，此事务数。 此文件包含所有文件或已添加到符号存储区在该事务期间的指针的列表。 如果删除事务，则 SymStore 将读取通过其事务文件以确定哪些文件和指针它应删除。

**外**并**del**选项用于指定是否要执行添加或删除事务。 包括 **/p**与添加操作的选项指定一个指针，是要添加; 省略 **/p**选项指定的实际符号文件是要添加。

还有可能在两个单独的阶段中创建符号存储区。 在第一阶段，您将使用与 SymStore **/x**选项来创建索引文件。 在第二个阶段中，使用与 SymStore **/y**选项创建的文件或指针的实际存储区中的索引文件的信息。

这可以是非常有用的技术的原因有多种。 例如，这允许要很轻松地重新创建存储区以某种方式将丢失，只要索引文件仍存在的符号存储区。 或者可能是包含符号文件的计算机具有慢速网络连接到计算机将在其创建符号存储区。 在这种情况下，可以创建符号文件所在的同一计算机上的索引文件、 索引文件传输到第二台计算机，然后在第二台计算机上创建存储。

有关 SymStore 的所有参数的完整列表，请参阅[ **SymStore 命令行选项**](symstore-command-line-options.md)。

**请注意**   SymStore 不支持从多个用户同时事务。 建议一个用户将指定的符号的"管理员"存储和负责所有**添加**并**del**事务。

 

### <a name="span-idtransactionexamplesspanspan-idtransactionexamplesspantransaction-examples"></a><span id="transaction_examples"></span><span id="TRANSACTION_EXAMPLES"></span>事务示例

下面是两个示例的添加生成 2195年的 Windows 2000 的符号指针的 SymStore \\ \\MyDir\\symsrv:

```console
symstore add /r /p /f \\BuildServer\BuildShare\2195free\symbols\*.* /s \\MyDir\symsrv /t "Windows 2000" /v "Build 2195 x86 free" /c "Sample add"
symstore add /r /p /f \\BuildServer\BuildShare\2195free\symbols\*.* /s \\MyDir\symsrv /t "Windows 2000" /v "Build 2195 x86 checked" /c "Sample add"
```

在以下示例中，SymStore 添加的应用程序项目中的实际符号文件\\ \\largeapp\\appserver\\到会\\ \\MyDir\\symsrv:

```console
symstore add /r /f \\largeapp\appserver\bins\*.* /s \\MyDir\symsrv /t "Large Application" /v "Build 432" /c "Sample add"
```

下面是如何使用索引文件的示例。 首先，SymStore 创建基于集合中的符号文件的索引文件\\ \\largeapp\\appserver\\箱\\。 在这种情况下，索引文件都放置在第三台计算机\\\\中心服务器\\hubshare。 您使用 **/g**选项以指定该文件作为前缀"\\\\largeapp\\appserver"可能会在将来更改：

```console
symstore add /r /p /g \\largeapp\appserver /f \\largeapp\appserver\bins\*.* /x \\hubserver\hubshare\myindex.txt
```

现在假设您将从计算机的所有符号文件都移\\ \\largeapp\\应用服务器并将其放\\ \\myarchive\\应用服务器。 然后可以从索引文件创建符号存储区本身\\\\中心服务器\\hubshare\\myindex.txt，如下所示：

```console
symstore add /y \\hubserver\hubshare\myindex.txt /g \\myarchive\appserver /s \\MyDir\symsrv /p /t "Large Application" /v "Build 432" /c "Sample Add from Index"
```

最后，下面是 SymStore 删除由先前的事务添加的文件的示例。 请参阅下面有关如何确定事务 ID （在此情况下，0000000096） 的说明的"server.txt 和 history.txt 文件"部分。

```console
symstore del /i 0000000096 /s \\MyDir\symsrv
```

### <a name="span-idtheservertxtandhistorytxtfilesspanspan-idtheservertxtandhistorytxtfilesspanthe-servertxt-and-historytxt-files"></a><span id="the_server_txt_and_history_txt_files"></span><span id="THE_SERVER_TXT_AND_HISTORY_TXT_FILES"></span>Server.txt 和 history.txt 文件

添加事务，多个项的信息添加到 server.txt 和 history.txt 将来查找功能。 下面是行的在 server.txt 和 history.txt 添加事务的一个示例：

```text
0000000096,add,ptr,10/09/99,00:08:32,Windows Vista SP 1,x86 fre 1.156c-RTM-2,Added from \\mybuilds\symbols,
```

这是以逗号分隔行。 这些字段进行了说明，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0000000096</p></td>
<td align="left"><p>事务 ID 号，因为由 SymStore 创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p>添加</p></td>
<td align="left"><p>事务的类型。 此字段可以是<strong>添加</strong>或<strong>del</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ptr</p></td>
<td align="left"><p>是否已添加文件或指针。 此字段可以是<strong>文件</strong>或<strong>ptr</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10/09/99</p></td>
<td align="left"><p>事务发生的日期。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>00:08:32</p></td>
<td align="left"><p>事务开始时的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista SP 1</p></td>
<td align="left"><p>产品。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>x86 如 fre</p></td>
<td align="left"><p>版本 （可选）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>添加从</p></td>
<td align="left"><p>注释 （可选）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>未使用</p></td>
<td align="left"><p>（保留以供将来使用。）</p></td>
</tr>
</tbody>
</table>

 

下面是从事务文件 0000000096 一些示例行。 每行记录在目录和文件或已添加到目录的指针的位置。

```text
canon800.dbg\35d9fd51b000,\\mybuilds\symbols\sp4\dll\canon800.dbg
canonlbp.dbg\35d9fd521c000,\\mybuilds\symbols\sp4\dll\canonlbp.dbg
certadm.dbg\352bf2f48000,\\mybuilds\symbols\sp4\dll\certadm.dbg
certcli.dbg\352bf2f1b000,\\mybuilds\symbols\sp4\dll\certcli.dbg
certcrpt.dbg\352bf04911000,\\mybuilds\symbols\sp4\dll\certcrpt.dbg
certenc.dbg\352bf2f7f000,\\mybuilds\symbols\sp4\dll\certenc.dbg
```

如果您使用**del**事务来撤销原始**添加**事务将从 server.txt，删除这些行和将到 history.txt 添加以下行：

```text
0000000105,del,0000000096
```

删除事务的字段如下所述。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0000000105</p></td>
<td align="left"><p>事务 ID 号，因为由 SymStore 创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p>del</p></td>
<td align="left"><p>事务的类型。 此字段可以是<strong>添加</strong>或<strong>del</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0000000096</p></td>
<td align="left"><p>已删除的事务。</p></td>
</tr>
</tbody>
</table>

 

 

 





