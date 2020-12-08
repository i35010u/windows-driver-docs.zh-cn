---
title: SymStore 事务
description: SymStore 事务
keywords:
- SymStore，事务
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 981c4cb955ed793ee9513de3e855fbc4b7bc0f81
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813927"
---
# <a name="symstore-transactions"></a>SymStore 事务


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


对 SymStore 的每次调用都记录为一个事务。 有两种类型的事务：添加和删除。

创建符号存储区时，会在服务器的根目录下创建名为 "000admin" 的目录。 000admin 目录包含每个事务的一个文件，以及日志文件 server.txt 和 history.txt。 server.txt 文件包含当前服务器上的所有事务的列表。 history.txt 文件包含所有事务的按时间排序的历史记录。

每次 SymStore 存储或删除符号文件时，都将创建一个新的事务号。 然后，在000admin 中创建一个文件，其名称为此事务号。 此文件包含在此事务中添加到符号存储区的所有文件或指针的列表。 如果删除了某个事务，SymStore 将读取其事务文件，以确定应删除的文件和指针。

" **添加** " **和 "** 删除" 选项指定是否要执行添加或删除事务。 包含带有 add 操作的 **/p** 选项可指定要添加的指针;如果省略 **/p** 选项，则指定要添加实际的符号文件。

还可以在两个不同的阶段创建符号存储区。 在第一个阶段中，将 SymStore 与 **/x** 选项一起使用来创建索引文件。 在第二阶段，使用带有 **/y** 选项的 SymStore 从索引文件中的信息创建文件或指针的实际存储。

由于各种原因，这可能是一项有用的技术。 例如，只要索引文件仍然存在，这就可以轻松地重新创建符号存储区。 或者，包含符号文件的计算机的网络连接速度慢于将在其上创建符号存储区的计算机。 在这种情况下，可以在与符号文件相同的计算机上创建索引文件，将索引文件传输到第二台计算机，然后在第二台计算机上创建该存储。

有关所有 SymStore 参数的完整列表，请参阅 [**SymStore Command-Line 选项**](symstore-command-line-options.md)。

**注意**   SymStore 不支持多个用户同时执行的事务。 建议将一个用户指定为符号存储的 "管理员"，并负责所有 **添加** 和 **全部事务。**

 

### <a name="span-idtransaction_examplesspanspan-idtransaction_examplesspantransaction-examples"></a><span id="transaction_examples"></span><span id="TRANSACTION_EXAMPLES"></span>事务示例

下面是两个 SymStore 示例，用于将2195的生成2000的符号指针添加到 \\ \\ MyDir \\ symsrv：

```console
symstore add /r /p /f \\BuildServer\BuildShare\2195free\symbols\*.* /s \\MyDir\symsrv /t "Windows 2000" /v "Build 2195 x86 free" /c "Sample add"
symstore add /r /p /f \\BuildServer\BuildShare\2195free\symbols\*.* /s \\MyDir\symsrv /t "Windows 2000" /v "Build 2195 x86 checked" /c "Sample add"
```

在下面的示例中，SymStore 将 largeapp microsoft.windows.appserver.2008 bin 中的应用程序项目的实际符号文件添加 \\ \\ \\ \\ 到 \\ \\ MyDir \\ symsrv：

```console
symstore add /r /f \\largeapp\appserver\bins\*.* /s \\MyDir\symsrv /t "Large Application" /v "Build 432" /c "Sample add"
```

下面是如何使用索引文件的示例。 首先，SymStore 基于 \\ \\ largeapp \\ microsoft.windows.appserver.2008 \\ 箱中的符号文件集合创建索引文件 \\ 。 在这种情况下，索引文件放在第三台计算机上，即 \\ \\ hubserver \\ hubshare。 使用 **/g** 选项来指定文件前缀 " \\ \\ largeapp \\ microsoft.windows.appserver.2008" 将来可能会更改：

```console
symstore add /r /p /g \\largeapp\appserver /f \\largeapp\appserver\bins\*.* /x \\hubserver\hubshare\myindex.txt
```

现在假设你将所有符号文件移出计算机 \\ \\ largeapp \\ microsoft.windows.appserver.2008，并将其放在 \\ \\ myarchive \\ microsoft.windows.appserver.2008。 然后，可以按如下所示从索引文件 \\ \\ hubserver \\ hubsharemyindex.txt 创建符号存储区 \\ ：

```console
symstore add /y \\hubserver\hubshare\myindex.txt /g \\myarchive\appserver /s \\MyDir\symsrv /p /t "Large Application" /v "Build 432" /c "Sample Add from Index"
```

最后，下面的示例说明了如何删除先前事务中添加的文件 SymStore。 请参阅下面的 "server.txt 和 history.txt 文件" 部分，了解有关如何确定事务 ID 的说明 (在本例中为 0000000096) 。

```console
symstore del /i 0000000096 /s \\MyDir\symsrv
```

### <a name="span-idthe_server_txt_and_history_txt_filesspanspan-idthe_server_txt_and_history_txt_filesspanthe-servertxt-and-historytxt-files"></a><span id="the_server_txt_and_history_txt_files"></span><span id="THE_SERVER_TXT_AND_HISTORY_TXT_FILES"></span>server.txt 和 history.txt 文件

添加事务后，会将多个信息添加到 server.txt 和 history.txt 中，以供将来查找功能使用。 下面是添加事务 server.txt 和 history.txt 中的行的示例：

```text
0000000096,add,ptr,10/09/99,00:08:32,Windows Vista SP 1,x86 fre 1.156c-RTM-2,Added from \\mybuilds\symbols,
```

这是一个以逗号分隔的行。 这些字段的说明如下所示：

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
<td align="left"><p>事务 ID 号，由 SymStore 创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p>add</p></td>
<td align="left"><p>事务的类型。 此字段可以为 " <strong>添加</strong> " 或 " <strong>del</strong>"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ptr</p></td>
<td align="left"><p>是否添加了文件或指针。 此字段可以是 <strong>file</strong> 或 <strong>ptr</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10/09/99</p></td>
<td align="left"><p>事务发生的日期。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>00:08:32</p></td>
<td align="left"><p>事务启动的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista SP 1</p></td>
<td align="left"><p>产品。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>x86 如 fre</p></td>
<td align="left"><p>版本 (可选) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>添加自</p></td>
<td align="left"><p>注释 (可选) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>未使用</p></td>
<td align="left"><p> (保留以供以后使用。 ) </p></td>
</tr>
</tbody>
</table>

 

下面是事务文件0000000096中的一些示例行。 每行记录目录以及已添加到目录中的文件或指针的位置。

```text
canon800.dbg\35d9fd51b000,\\mybuilds\symbols\sp4\dll\canon800.dbg
canonlbp.dbg\35d9fd521c000,\\mybuilds\symbols\sp4\dll\canonlbp.dbg
certadm.dbg\352bf2f48000,\\mybuilds\symbols\sp4\dll\certadm.dbg
certcli.dbg\352bf2f1b000,\\mybuilds\symbols\sp4\dll\certcli.dbg
certcrpt.dbg\352bf04911000,\\mybuilds\symbols\sp4\dll\certcrpt.dbg
certenc.dbg\352bf2f7f000,\\mybuilds\symbols\sp4\dll\certenc.dbg
```

如果使用 **del** 事务来撤消原始 **添加** 事务，将从 server.txt 中删除这些行，并将以下行添加到 history.txt：

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
<td align="left"><p>事务 ID 号，由 SymStore 创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p>del</p></td>
<td align="left"><p>事务的类型。 此字段可以为 " <strong>添加</strong> " 或 " <strong>del</strong>"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0000000096</p></td>
<td align="left"><p>已删除的事务。</p></td>
</tr>
</tbody>
</table>

 

 

 





