---
title: PoolMon 示例
description: PoolMon 示例
ms.assetid: aff0abdd-7d68-49b8-b9a1-71ab866c8487
keywords:
- PoolMon WDK 示例
- 内存池监视器 WDK 示例
- 示例 WDK PoolMon
ms.date: 07/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb6caa7e3d4773a60f19f324e7dd87e1f04452d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577281"
---
# <a name="poolmon-examples"></a>PoolMon 示例


## <span id="ddk_poolmon_examples_tools"></span><span id="DDK_POOLMON_EXAMPLES_TOOLS"></span>


本主题包括 PoolMon 使用以下示例：

示例 1：显示和 PoolMon 输出进行排序

示例 2：显示驱动程序名称

示例 3：检测内存泄漏

示例 4：检查池内存泄漏

示例 5：监视终端服务器会话

### <a name="span-idddkexample1displayandsortpoolmonoutputtoolsspanspan-idddkexample1displayandsortpoolmonoutputtoolsspanexample-1-display-and-sort-poolmon-output"></a><span id="ddk_example_1_display_and_sort_poolmon_output_tools"></span><span id="DDK_EXAMPLE_1_DISPLAY_AND_SORT_POOLMON_OUTPUT_TOOLS"></span>示例 1:显示和 PoolMon 输出进行排序

此示例介绍了通过多种方式配置 PoolMon 显示。 默认情况下，PoolMon 显示所有内核内存分配，以字母数字顺序按标记值。 可以修改显示在命令行或 PoolMon 正在运行时的排序顺序。

以下命令启动 PoolMon:

```
poolmon
```

以下命令启动 PoolMon，并显示按 free 操作的数目：

```
poolmon /f
```

在运行时 poolmon，可以使用运行命令来更改显示。 例如，若要使用的字节数排序显示，请按**b**。 若要按每个分配的字节进行排序，按**m**。

以下命令启动 PoolMon 并显示仅从非分页缓冲池的分配：

```
poolmon /p
```

在运行时 PoolMon，按**p**切换通过从页面缓冲的池和 / 或非分页的池的分配。

若要启动 PoolMon 并显示具有特定标记的分配的数据，请使用 **/i**参数。 下面的命令显示分配，则使用**AfdB**标记 （由用于数据缓冲区的 afd.sys 标记）。

```
poolmon /iAfdB
```

若要排除具有特定标记的分配，请使用 **/x**参数。 下面的命令显示所有不具有的分配**AfdB**标记;

```
poolmon /xAfdB
```

可以使用星号 (\*) 和/或问号 （？） 来指定一组标记包含相同字符。 下面的命令显示了池标记开头的分配**Afd**，afd.sys; 使用的标记

```
poolmon /iAfd*
```

PoolMon 启动命令可以包括多个 **/i**并 **/x**参数。 下面的命令显示已标记开头的分配**Aud**和四个字符标记开头**Cc**，除了分配，则使用**CcBc**标记;

```
poolmon /iAud* /iCc?? /xCcBc
```

此外可以对 PoolMon 显示在更新之间的值更改进行排序。 **/ (** 参数将 PoolMon 放在排序通过更改模式。

下面的命令显示分配与标记开头**Afd**，并对所分配的更改进行排序。 它使用 **/a**参数要作为排序依据的分配数和 **/)** 参数要作为排序依据的分配数的更改。

```
poolmon /iAfd* /( /a
```

**/ (** 参数和括号键是切换开关。 通过更改排序模式 PoolMon 时，它将所有排序命令都解释为命令要作为排序依据的值更改。 如果再次按下括号键，它对排序值。

### <a name="span-idddkexample2displaydrivernamestoolsspanspan-idddkexample2displaydrivernamestoolsspanexample-2-display-driver-names"></a><span id="ddk_example_2_display_driver_names_tools"></span><span id="DDK_EXAMPLE_2_DISPLAY_DRIVER_NAMES_TOOLS"></span>示例 2:显示驱动程序名称

您可以使用 PoolMon **/g**参数来显示名称的 Windows 组件和通常用于分配每个池标记的驱动程序。 如果分配了特定标记的已发现问题，此功能可帮助你确定有问题的组件或驱动程序。

在映射中列出的组件和驱动程序\_驱动程序列中，在显示中最右侧的列。 映射的数据\_驱动程序列来自 pooltag.txt，随 PoolMon 一起安装的文件。

下面的命令显示使用开头的标记分配的内存**NtF**。 (它使用问号字符 (**？**) 作为通配符。)**/G**参数将添加映射\_驱动程序列。

```
poolmon /iNtF? /g
```

生成的显示列标记从分配**NtF**。 在显示中，最右侧的列映射\_驱动程序，演示，已分配的内存 ntfs.sys，NTFS 文件系统的驱动程序。 在这种情况下，显示为甚至更具体，因为 pooltag.txt 包括 NTFS 分配的源代码文件。

```
 Memory:  260620K Avail:   65152K  PageFlts:    85   InRam Krnl: 2116K P:19560K
 Commit: 237688K Limit: 640916K Peak: 260632K            Pool N: 8500K P:33024K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 NtFA Nonp       9112 (   0)      9112 (   0)     0       0 (     0)      0 [ntfs.sys  -  AttrSup.c]
 NtFB Paged      3996 (   0)      3986 (   0)    10  252088 (     0)  25208 [ntfs.sys  -  BitmpSup.c]
 NtFC Paged   1579279 (   0)   1579269 (   0)    10     640 (     0)     64 [ntfs.sys  -  Create.c]
 NtFD Nonp         13 (   0)        13 (   0)     0       0 (     0)      0 [ntfs.sys  -  DevioSup.c]
 NtFF Paged      1128 (   0)      1128 (   0)     0       0 (     0)      0 [ntfs.sys  -  FileInfo.c]
 NtFI Nonp        152 (   0)       152 (   0)     0       0 (     0)      0 [ntfs.sys  -  IndexSup.c]
 NtFL Nonp      68398 (   0)     68390 (   0)     8   27280 (     0)   3410 [ntfs.sys  -  LogSup.c]
 NtFS Paged      2915 (   0)      2614 (   0)   301   80192 (     0)    266 [ntfs.sys  -  SecurSup.c]
 NtFa Paged       838 (   0)       829 (   0)     9     288 (     0)     32 [ntfs.sys  -  AllocSup.c]
 NtFd Paged    137696 (   0)    137688 (   0)     8     720 (     0)     90 [ntfs.sys  -  DirCtrl.c]
 NtFf Nonp          2 (   0)         1 (   0)     1      40 (     0)     40 [ntfs.sys  -  FsCtrl.c]
 NtFs Nonp      48825 (   0)     47226 (   0)  1599   64536 (     0)     40 [ntfs.sys  -  StrucSup.c]
 NtFv Paged       551 (   0)       551 (   0)     0       0 (     0)      0 [ntfs.sys  -  ViewSup.c]
```

Pooltag.txt 很广泛，但它不是在 Windows 中使用的所有标记的完整列表。 PoolMon 中 pooltag.txt 未包含在显示的标记，在映射中显示"未知驱动程序"\_标记的驱动程序列。 当发生这种情况时，可以使用 **/c**参数搜索在本地系统上的驱动程序，并确定它们是否将标记分配。

下面的示例演示此方法。

下面的命令使用 **/i**参数列表分配，则使用结束中内存优化的标记。 **/G**参数从 pooltag.txt 文件将驱动程序名称添加到显示。

```
poolmon /i?MEM /g
```

生成的显示与尾号为内存优化的标记列出了分配。 但是，因为内存优化标记不包含在 pooltag.txt，就会在映射中显示"未知驱动程序"\_驱动程序而不是驱动程序名称的列。

```
 Tag  Type        Allocs          Frees      Diff   Bytes      Per Alloc    Mapped_Driver

 1MEM Nonp       1 (   0)         0 (   0)     1    3344 (     0)   3344   Unknown Driver
 2MEM Nonp       1 (   0)         0 (   0)     1    3944 (     0)   3944   Unknown Driver
 3MEM Nonp       3 (   0)         0 (   0)     3     248 (     0)     82   Unknown Driver
```

在这种情况下，可以使用 **/c**参数来编译的本地驱动程序和他们分配的标记的列表，然后在映射中显示的名称的本地驱动程序\_驱动程序列。

以下命令启动 PoolMon。 它使用 **/i**加上内存优化，以结尾的标记列表分配到的参数和 **/c**参数来显示分配标记的本地驱动程序。

```
poolmon /i?MEM /c
```

如果未指定本地标记文件和 PoolMon 找不到 localtag.txt 文件，它将创建一个，如以下屏幕上的信息中所示。 （PoolMon 不能生成 64 位版本的 Windows 上的本地标记文件）。

```
d:\tools\poolmon>poolmon /?MEM /c
PoolMon: No localtag.txt in current directory
PoolMon: Creating localtag.txt in current directory......
```

使用新创建的 localtag.txt 文件中的内容，在结果显示在映射中显示的本地驱动程序名称\_驱动程序列。

```
 Memory:  260620K Avail:   57840K  PageFlts:   162   InRam Krnl: 2116K P:19448K
 Commit: 244580K Limit: 640916K Peak: 265416K            Pool N: 8496K P:32904K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 1MEM Nonp          1 (   0)         0 (   0)        1    3344 (     0)   3344 [el90xbc5]
 2MEM Nonp          1 (   0)         0 (   0)        1    3944 (     0)   3944 [el90xbc5]
 3MEM Nonp          3 (   0)         0 (   0)        3     248 (     0)     82 [el90xbc5]
```

对于综合的驱动程序名称显示，可将合并 **/c**并 **/g**命令中的参数。 （参数的顺序不更改输出）。以下命令将列出分配的标记开头**Ip**。 它使用 **/c**参数，它使用映射中的 localtag.txt 文件的内容\_驱动程序列和 **/g**参数，它使用映射中的 pooltag.txt 文件的内容\_驱动程序列。

```
poolmon /iIp* /c /g
```

在生成的显示中，映射\_驱动程序列包含 localtag.txt 和 pooltag.txt 文件中的数据。

```
 Memory:  130616K Avail:   23692K  PageFlts:   146   InRam Krnl: 2108K P: 9532K
 Commit: 187940K Limit: 318628K Peak: 192000K            Pool N: 8372K P:13384K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 IpEQ Nonp          1 (   0)         0 (   0)        1    1808 (     0)   1808 [ipsec][ipsec.sys    -  event queue]
 IpFI Nonp         26 (   0)         0 (   0)       26    7408 (     0)    284 [ipsec][ipsec.sys    -  Filter blocks]
 IpHP Nonp          1 (   0)         1 (   0)        0       0 (     0)      0 [ipsec.sys    - IP Security]
 IpIO Nonp          1 (   0)         1 (   0)        0       0 (     0)      0 [ipsec]
 IpLA Nonp          1 (   0)         0 (   0)        1     248 (     0)    248 [ipsec][ipsec.sys    -  lookaside lists]
 IpSH Nonp          1 (   0)         1 (   0)        0       0 (     0)      0 [ipsec.sys    - IP Security]
 IpSI Nonp       1027 (   0)         0 (   0)     1027   53272 (     0)     51 [ipsec][ipsec.sys    - initial allcoations]
 IpTI Nonp          3 (   0)         0 (   0)        3    5400 (     0)   1800 [ipsec][ipsec.sys    -  timers]
```

### <a name="span-idddkexample3detectmemoryleakagetoolsspanspan-idddkexample3detectmemoryleakagetoolsspanexample-3-detect-memory-leakage"></a><span id="ddk_example_3_detect_memory_leakage_tools"></span><span id="DDK_EXAMPLE_3_DETECT_MEMORY_LEAKAGE_TOOLS"></span>示例 3:检测内存泄漏

此示例中所示使用 PoolMon 来检测内存泄漏的过程。

1.  使用参数启动 PoolMon **/p/p** （显示仅从页面缓冲池分配） 和**b </b** （按字节数）。
    ```
    poolmon /p /p /b
    ```

2.  让 PoolMon 运行了几个小时。 起始 PoolMon 更改的数据，因为它是可靠的数据之前必须重新获得稳定状态。

3.  保存的屏幕截图，或从命令窗口中复制并将其粘贴到记事本 PoolMon，生成的信息。

4.  返回到 PoolMon，按**p**键两次以显示仅从非分页缓冲池分配。

5.  重复步骤 3 和 4 大约每半小时至少两个小时，分页和非分页池显示每个时间之间进行切换。

6.  数据收集完成后，检查的差异 （减去免费操作分配操作） 和字节 （分配的释放的字节数减去的字节数） 为每个值标记，并记下任何持续增加。

7.  接下来，停止 PoolMon，等待几个小时，然后重新启动 PoolMon。

8.  检查已增加，并确定是否将字节现在也将释放的分配。 可能的原因是分配不仍已释放或不断增加的大小。


### <a name="span-idddkexample4examineapoolmemoryleaktoolsspanspan-idddkexample4examineapoolmemoryleaktoolsspanexample-4-examine-a-pool-memory-leak"></a><span id="ddk_example_4_examine_a_pool_memory_leak_tools"></span><span id="DDK_EXAMPLE_4_EXAMINE_A_POOL_MEMORY_LEAK_TOOLS"></span>示例 4:检查池内存泄漏

下面的示例演示如何使用 PoolMon 调查可疑的打印机驱动程序从池内存泄漏。 在此示例中，PoolMon 显示 Windows 会收集有关内存分配，则使用 Dsrd 标记的数据。

打印机驱动程序分配 Drsd 标记时它们将图形设备接口 (GDI) 对象和相关联的内存分配。 如果打印机驱动程序可能具有对象泄漏，Drsd 标记与分配的内存也将会泄漏。

**请注意**  之前在此示例中运行的步骤，请确保只有在完成后不会中断正在使用的打印机。 否则，结果可能无效。

 

在命令行中，键入以下命令：

```
poolmon /iDrsd
```

此命令将定向 PoolMon 显示分配，则使用 Drsd 标记的信息。 （池标记是区分大小写，因此请确保严格按照所示键入命令。）

在差异和 Bytes 列中记录的值。 在以下示例显示中，差异的值为 21 和字节数是 17472。

```
Memory:  130480K Avail:   91856K  PageFlts:  1220   InRam Krnl: 2484K P: 7988K
Commit:  30104K Limit: 248432K Peak:  34028K            Pool N: 2224K P: 8004K
Tag  Type        Allocs           Frees           Diff  Bytes           Per Alloc

Drsd Paged       560 ( 177)       539 ( 171)       21   17472 (  4992)    832 
```

向打印机发送作业，短暂地等待 Windows 以返回到正常，然后记录的差异和字节列的值。

```
Memory:  130480K Avail:   91808K  PageFlts:  1240   InRam Krnl: 2488K P: 7996K
Commit:  30152K Limit: 248432K Peak:  34052K            Pool N: 2224K P: 8012K
Tag  Type        Allocs           Frees           Diff  Bytes          Per Alloc

Drsd Paged       737 (   0)       710 (   0)       27   22464 (     0)    832  
```

时的内存管理的打印机驱动程序正常工作，差异的值应打印完成后，返回到其原始值为 21。 但是，与上面的输出所示，差异玫瑰 27、 和的玫瑰 22464 到的字节数的值。 初始和后续输出之间的差异意味着采用 4992 字节，总共 6 个 Drsd 块泄漏在打印期间。

### <a name="span-idformoreinformationspanspan-idformoreinformationspanspan-idformoreinformationspanfor-more-information"></a><span id="For_More_Information"></span><span id="for_more_information"></span><span id="FOR_MORE_INFORMATION"></span>有关详细信息

如果您认为您已确定泄漏的驱动程序，请转到[Microsoft 支持部门](https://go.microsoft.com/fwlink/p/?linkid=8713)网站，搜索知识库相关文章。

### <a name="span-idddkexample5monitoraterminalserversessiontoolsspanspan-idddkexample5monitoraterminalserversessiontoolsspanexample-5-monitor-a-terminal-server-session"></a><span id="ddk_example_5_monitor_a_terminal_server_session_tools"></span><span id="DDK_EXAMPLE_5_MONITOR_A_TERMINAL_SERVER_SESSION_TOOLS"></span>示例 5:监视终端服务器会话

此示例演示几个方式显示从终端服务会话池分配。 它演示如何使用 **/s**命令行参数，并**s**， *TSSessionID*，以及**我**运行参数。

下面的命令显示所有终端服务会话池分配。 在此示例中，本地计算机，配置为终端服务器，将托管会话，而客户端计算机使用远程桌面功能来连接到主机。

```
poolmon /s
```

在响应中，poolmon 可显示从所有会话池分配。 请注意在标头中的"所有会话都池信息"标题。

```
Memory:  523572K Avail:  233036K  PageFlts:   344   InRam Krnl: 1828K P:18380K
Commit: 193632K Limit:1279764K Peak: 987356K            Pool N:14332K P:18644K
All sessions pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Bmfd Paged       361 (   0)       336 (   0)       25   57832 (     0)   2313
 DDfb Paged        34 (   0)        22 (   0)       12     720 (     0)     60
 Dddp Paged         8 (   0)         6 (   0)        2     272 (     0)    136
 Dh 1 Paged        24 (   0)        24 (   0)        0       0 (     0)      0
 Dh 2 Paged       344 (   0)       344 (   0)        0       0 (     0)      0
 Dvgr Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 GDev Paged       108 (   0)       102 (   0)        6   20272 (     0)   3378
 GFil Paged        29 (   0)        27 (   0)        2     160 (     0)     80
 GPal Paged        11 (   0)         8 (   0)        3     816 (     0)    272
 GTmp Paged     88876 (   1)     88876 (   1)        0       0 (     0)      0
 GUma Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 Galp Paged      3250 (   0)      3250 (   0)        0       0 (     0)      0
 Gbaf Paged      9829 (   0)      9801 (   0)       28   19712 (     0)    704
 Gcac Paged      3761 (   0)      3706 (   0)       55  288968 (     0)   5253
 Gcsl Paged         1 (   0)         0 (   0)        1     488 (     0)    488
 Gdbr Paged      6277 (   0)      6271 (   0)        6    1872 (     0)    312
 ...
```

若要查看从特定的会话池分配，请键入的会话 ID 之后立即 **/s**参数，如以下命令中所示。 此命令显示终端服务会话 0 的会话池分配。

```
poolmon /s0
```

在响应中，PoolMon 显示的终端服务会话 0 中分配的会话池。 请注意在标头中的"会话 0 池信息"标题。

```
Memory:  523572K Avail:  233024K  PageFlts:   525   InRam Krnl: 1828K P:18384K
 Commit: 193760K Limit:1279764K Peak: 987356K            Pool N:14340K P:18644K
 Session 0 pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Bmfd Paged       361 (   0)       336 (   0)       25   57832 (     0)   2313
 DDfb Paged        34 (   0)        22 (   0)       12     720 (     0)     60
 Dddp Paged         8 (   0)         6 (   0)        2     272 (     0)    136
 Dh 1 Paged        24 (   0)        24 (   0)        0       0 (     0)      0
 Dh 2 Paged       344 (   0)       344 (   0)        0       0 (     0)      0
 Dvgr Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 GDev Paged       108 (   0)       102 (   0)        6   20272 (     0)   3378
 GFil Paged        29 (   0)        27 (   0)        2     160 (     0)     80
 GPal Paged        11 (   0)         8 (   0)        3     816 (     0)    272
 GTmp Paged     89079 (  99)     89079 (  99)        0       0 (     0)      0
 GUma Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 Galp Paged      3250 (   0)      3250 (   0)        0       0 (     0)      0
 Gbaf Paged      9830 (   0)      9802 (   0)       28   19712 (     0)    704
 Gcac Paged      3762 (   0)      3707 (   0)       55  283632 (     0)   5156
 Gcsl Paged         1 (   0)         0 (   0)        1     488 (     0)    488
 Gdbr Paged      6280 (   0)      6274 (   0)        6    1872 (     0)    312
 ...
```

若要帮助确定哪些驱动程序和组件从会话池分配内存，将添加 **/g**参数，如以下命令中所示。 **/G**参数将添加映射\_列出的 Windows 组件和分配每个标记的驱动程序的驱动程序列。

```
poolmon /s0 /g

Memory:  523572K Avail:  235876K  PageFlts:    43   InRam Krnl: 1900K P:18860K
Commit: 185040K Limit:1279764K Peak: 987356K            Pool N:14684K P:19124K
Session 0 pool information
Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

Bmfd Paged       421 (   0)       396 (   0)       25   57832 (     0)   2313 [Font related stuff]
DDfb Paged        34 (   0)        22 (   0)       12     720 (     0)     60 Unknown Driver
Dddp Paged        11 (   0)         6 (   0)        5     392 (     0)     78 Unknown Driver
Dh 1 Paged        37 (   0)        35 (   0)        2     224 (     0)    112 Unknown Driver
Dh 2 Paged       367 (   0)       364 (   0)        3     912 (     0)    304 Unknown Driver
Dvgr Paged         2 (   0)         2 (   0)        0       0 (     0)      0 [vga for risc video driver]
GDev Paged       119 (   0)       113 (   0)        6   20272 (     0)   3378 [Gdi pdev]
GFil Paged        29 (   0)        27 (   0)        2     160 (     0)     80 [Gdi engine descriptor list]
GPal Paged        11 (   0)         8 (   0)        3     816 (     0)    272 [Gdi Objects]
GTmp Paged     98626 (   1)     98626 (   1)        0       0 (     0)      0 [Gdi Objects]
GUma Paged         2 (   0)         2 (   0)        0       0 (     0)      0 [Gdi Objects]
Galp Paged      3250 (   0)      3250 (   0)        0       0 (     0)      0 [Gdi Objects]
Gbaf Paged     10331 (   0)     10305 (   0)       26   18304 (     0)    704 [Gdi Objects]
Gcac Paged      4722 (   0)      4666 (   0)       56  305400 (     0)   5453 [Gdi glyph cache]
Gcsl Paged         1 (   0)         0 (   0)        1     488 (     0)    488 [Gdi string resource script names]
Gdbr Paged      6972 (   0)      6965 (   0)        7    2184 (     0)    312 [Gdi driver brush realization]
```

PoolMon 正在运行时，还可以配置终端服务会话池显示。 下表显示了一系列的运行命令，在其中键入的顺序和生成的 PoolMon 显示中。

包含一个用于启动 PoolMon 开始序列。 PoolMon 正在运行时，所有其他参数的类型。

```
poolmon
```

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键</th>
<th align="left">结果</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>显示所有会话池。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>显示系统池。</p></td>
<td align="left"><p><strong>S</strong>参数将显示系统池和终端服务会话池之间切换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>显示会话 0 池。</p></td>
<td align="left"><p>显示系统池时，可以键入一个会话 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>7</strong></p></td>
<td align="left"><p>显示会话 7 池。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>a</strong></p></td>
<td align="left"><p>显示池分配的会话 7 中，按分配数。</p></td>
<td align="left"><p>所有标准的正在运行参数都是有效的会话池显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>显示分配用于 session 0，按分配数。</p></td>
<td align="left"><p>更改之前保留会话和排序选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>显示系统池。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>显示分配用于 session 0，按分配数。</p></td>
<td align="left"><p>保留会话选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>10ENTER</strong></p></td>
<td align="left"><p>显示会话 1 分配，然后显示会话 0 分配。</p></td>
<td align="left"><p>无需<strong>我</strong>，可以输入仅会话 Id 为 0 到 9。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>会提示你输入终端服务器会话 id。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>10</strong></p></td>
<td align="left"><p>显示会话 10 分配。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>会提示你输入终端服务器会话 id。</p></td>
<td align="left"><p>若要显示所有会话池，请按<strong>我</strong>，然后按 ENTER。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>输入</strong></p></td>
<td align="left"><p>显示所有会话池。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

仅系统配置为终端服务器会话池中分配的内存。 如果您使用 PoolMon 不是终端服务器的计算机上显示会话池或键入一个会话 ID 在 Windows 上不存在，PoolMon 不显示任何分配。 相反，它会显示仅与常规内存数据标题。

下面的命令显示从终端服务会话的所有池的分配：

```
poolmon /s
```

下图显示了时所产生的 PoolMon 显示器 **/s**命令已提交至运行无法配置为终端服务器的 Windows XP 的计算机：

```
 Memory:  260620K Avail:   44956K  PageFlts:   308   InRam Krnl: 2744K P:20444K
 Commit: 185452K Limit: 640872K Peak: 192472K            Pool N: 8112K P:20648K
 All sessions pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc
```

 

 





