---
title: PoolMon 示例
description: PoolMon 示例
ms.assetid: aff0abdd-7d68-49b8-b9a1-71ab866c8487
keywords:
- PoolMon WDK，示例
- 内存池监视器 WDK，示例
- 示例 WDK PoolMon
ms.date: 07/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: f033c410126cc798d1106aafdbbd570f49f85e56
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769373"
---
# <a name="poolmon-examples"></a>PoolMon 示例


## <span id="ddk_poolmon_examples_tools"></span><span id="DDK_POOLMON_EXAMPLES_TOOLS"></span>


本主题包括以下 PoolMon 使用示例：

示例1：显示和排序 PoolMon 输出

示例2：显示驱动程序名称

示例3：检测内存泄漏

示例4：检查池内存泄漏

示例5：监视终端服务器会话

### <a name="span-idddk_example_1_display_and_sort_poolmon_output_toolsspanspan-idddk_example_1_display_and_sort_poolmon_output_toolsspanexample-1-display-and-sort-poolmon-output"></a><span id="ddk_example_1_display_and_sort_poolmon_output_tools"></span><span id="DDK_EXAMPLE_1_DISPLAY_AND_SORT_POOLMON_OUTPUT_TOOLS"></span>示例1：显示和排序 PoolMon 输出

此示例介绍了配置 PoolMon 显示的各种方式。 默认情况下，PoolMon 按标记值以字母数字顺序显示所有内核内存分配。 你可以在命令行上或在 PoolMon 正在运行时修改显示的排序顺序。

以下命令启动 PoolMon：

```
poolmon
```

以下命令将启动 PoolMon，并按免费操作数对显示进行排序：

```
poolmon /f
```

当 poolmon 正在运行时，你可以使用运行时命令来更改显示。 例如，若要按使用的字节数排序显示，请按**b**。 若要按每个分配的字节排序，请按**m**。

以下命令启动 PoolMon 并仅显示非分页池的分配：

```
poolmon /p
```

当 PoolMon 正在运行时，按**p**可通过分页池的分配、非分页池或两者进行切换。

若要为具有特定标记的分配启动 PoolMon 并显示数据，请使用 **/i**参数。 以下命令显示具有**AfdB**标记（afd 用于数据缓冲区的标记）的分配。

```
poolmon /iAfdB
```

若要排除具有特定标记的分配，请使用 **/x**参数。 以下命令显示没有**AfdB**标记的所有分配;

```
poolmon /xAfdB
```

您可以使用星号（ \* ）和/或问号（？）来指定具有相同字符的一组标记。 以下命令显示具有以**Afd**开头的池标记、Afd 使用的标记的分配;

```
poolmon /iAfd*
```

PoolMon 启动命令可以包含多个 **/i**和 **/x**参数。 以下命令显示具有以**Aud**开头的标记和以**Cc**开头的四个字符标记之外的四个字符的分配，但使用**CcBc**标记的分配除外;

```
poolmon /iAud* /iCc?? /xCcBc
```

你还可以通过更新之间的值的更改对 PoolMon 显示进行排序。 **/（** 参数将 PoolMon 置于逐更改模式。

以下命令显示标记以**Afd**开头的分配，并按分配中的更改进行排序。 它使用 **/a**参数按分配数和 **/）** 参数进行排序，以按分配数的更改进行排序。

```
poolmon /iAfd* /( /a
```

**/（** 参数和括号键是切换开关。 当 PoolMon 处于按更改模式时，它会将所有排序命令解释为按值中的更改进行排序的命令。 如果再次按下括号键，则将按值排序。

### <a name="span-idddk_example_2_display_driver_names_toolsspanspan-idddk_example_2_display_driver_names_toolsspanexample-2-display-driver-names"></a><span id="ddk_example_2_display_driver_names_tools"></span><span id="DDK_EXAMPLE_2_DISPLAY_DRIVER_NAMES_TOOLS"></span>示例2：显示驱动程序名称

可以使用 PoolMon **/g**参数显示分配每个池标记的 Windows 组件和常用驱动程序的名称。 如果发现具有特定标记的分配有问题，此功能可帮助你确定问题的组件或驱动程序。

组件和驱动程序列在 "映射的 \_ 驱动程序" 列中显示的最右侧列中。 映射的 \_ 驱动程序列的数据来自 pooltag （使用 PoolMon 安装的文件）。

以下命令显示用以**contoso.ntf**开头的标记分配的内存。 （它使用问号字符（**？**）作为通配符。）**/G**参数添加映射的 \_ 驱动程序列。

```
poolmon /iNtF? /g
```

生成的显示列表以**contoso.ntf**开头的标记进行分配。 显示 "映射的驱动程序" 中最右边的列 \_ 显示该内存是由 ntfs 为 ntfs 文件系统的驱动程序分配的。 在这种情况下，显示内容更为具体，因为 pooltag 包含 NTFS 分配的源文件。

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

Pooltag 很多，但它不是 Windows 中使用的所有标记的完整列表。 当显示中显示的标记不包含在 pooltag 中时，PoolMon 会在标记的映射驱动程序列中显示 "未知驱动程序" \_ 。 出现这种情况时，可以使用 **/c**参数搜索本地系统上的驱动程序，并确定它们是否分配了标记。

下面的示例演示了此方法。

以下命令使用 **/i**参数列出了以 MEM 结尾的标记的分配。 **/G**参数将驱动程序名称从 pooltag 文件添加到显示中。

```
poolmon /i?MEM /g
```

生成的显示将列出标记以 MEM 结尾的分配。 但是，由于 pooltag 中未包含 MEM 标记，因此 "未知驱动程序" 会显示在 "映射的驱动程序" 列中， \_ 代替驱动程序名称。

```
 Tag  Type        Allocs          Frees      Diff   Bytes      Per Alloc    Mapped_Driver

 1MEM Nonp       1 (   0)         0 (   0)     1    3344 (     0)   3344   Unknown Driver
 2MEM Nonp       1 (   0)         0 (   0)     1    3944 (     0)   3944   Unknown Driver
 3MEM Nonp       3 (   0)         0 (   0)     3     248 (     0)     82   Unknown Driver
```

在这种情况下，可以使用 **/c**参数来编译本地驱动程序的列表及其分配的标记，然后在 "映射的驱动程序" 列中显示本地驱动程序的名称 \_ 。

以下命令启动 PoolMon。 它使用 **/i**参数列出标记以内存结尾的分配，并使用 **/c**参数显示分配标记的本地驱动程序。

```
poolmon /i?MEM /c
```

如果未指定本地标记文件，并且 PoolMon 找不到 localtag 文件，则会创建一个，如下面的屏幕消息中所示。 （PoolMon 无法在64位版本的 Windows 上生成本地标记文件。）

```
d:\tools\poolmon>poolmon /?MEM /c
PoolMon: No localtag.txt in current directory
PoolMon: Creating localtag.txt in current directory......
```

生成的显示将使用新创建的 localtag 文件中的内容，在 "映射的驱动程序" 列中显示本地驱动程序名称 \_ 。

```
 Memory:  260620K Avail:   57840K  PageFlts:   162   InRam Krnl: 2116K P:19448K
 Commit: 244580K Limit: 640916K Peak: 265416K            Pool N: 8496K P:32904K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 1MEM Nonp          1 (   0)         0 (   0)        1    3344 (     0)   3344 [el90xbc5]
 2MEM Nonp          1 (   0)         0 (   0)        1    3944 (     0)   3944 [el90xbc5]
 3MEM Nonp          3 (   0)         0 (   0)        3     248 (     0)     82 [el90xbc5]
```

若要显示完整的驱动程序名称，可以在命令中组合 **/c**和 **/g**参数。 （参数顺序不更改输出。）以下命令列出了以**Ip**开头的标记的分配。 它使用 **/c**参数，该参数使用映射的驱动程序列中 localtag 文件的内容 \_ 和 **/g**参数，该参数使用映射的 \_ 驱动程序列中 pooltag 文件的内容。

```
poolmon /iIp* /c /g
```

在生成的显示中，"映射的 \_ 驱动程序" 列包含来自 localtag 和 pooltag 文件的数据。

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

### <a name="span-idddk_example_3_detect_memory_leakage_toolsspanspan-idddk_example_3_detect_memory_leakage_toolsspanexample-3-detect-memory-leakage"></a><span id="ddk_example_3_detect_memory_leakage_tools"></span><span id="DDK_EXAMPLE_3_DETECT_MEMORY_LEAKAGE_TOOLS"></span>示例3：检测内存泄漏

此示例建议使用 PoolMon 检测内存泄漏的过程。

1.  使用参数 **/p/p** （仅显示分页池的分配）和 **/b** （按字节数排序）开始 PoolMon。
    ```
    poolmon /p /p /b
    ```

2.  让 PoolMon 运行几个小时。 由于启动 PoolMon 会更改数据，因此必须重新获得稳定状态，然后数据才会可靠。

3.  保存由 PoolMon 生成的信息，无论是屏幕截图，还是从命令窗口中复制并粘贴到记事本中。

4.  返回到 PoolMon，按两次**p**键，只显示非分页池的分配。

5.  大约每半小时重复执行步骤3和4，每隔两小时一次，每次都会显示分页和非分页池。

6.  数据收集完成后，请检查每个标记的差异（分配操作减去可用操作）和字节数（分配的字节数减去已释放的字节数），并记下持续增加的任何值。

7.  接下来，停止 PoolMon，等待几个小时，然后重启 PoolMon。

8.  检查已增加的分配，并确定是否现在释放字节。 可能的原因是仍未释放或持续增加大小的分配。


### <a name="span-idddk_example_4_examine_a_pool_memory_leak_toolsspanspan-idddk_example_4_examine_a_pool_memory_leak_toolsspanexample-4-examine-a-pool-memory-leak"></a><span id="ddk_example_4_examine_a_pool_memory_leak_tools"></span><span id="DDK_EXAMPLE_4_EXAMINE_A_POOL_MEMORY_LEAK_TOOLS"></span>示例4：检查池内存泄漏

下面的示例演示如何使用 PoolMon 来调查来自可疑打印机驱动程序的池内存泄露。 在此示例中，PoolMon 显示 Windows 收集的有关带有 Dsrd 标记的内存分配的数据。

打印机驱动程序在分配图形设备接口（GDI）对象和相关内存时分配 Drsd 标记。 如果打印机驱动程序有对象泄漏，则使用 Drsd 标记分配的内存也会泄漏。

**注意**   在运行此示例中的步骤之前，请确保你正在使用的打印机不会中断，直到你完成。 否则，结果可能无效。

 

在命令行中键入以下命令：

```
poolmon /iDrsd
```

此命令指示 PoolMon 显示带有 Drsd 标记的分配的信息。 （池标记区分大小写，因此请务必严格按所示键入命令。）

记录 Diff 和 Bytes 列中的值。 在下面的示例显示中，Diff 的值为21，字节数为17472。

```
Memory:  130480K Avail:   91856K  PageFlts:  1220   InRam Krnl: 2484K P: 7988K
Commit:  30104K Limit: 248432K Peak:  34028K            Pool N: 2224K P: 8004K
Tag  Type        Allocs           Frees           Diff  Bytes           Per Alloc

Drsd Paged       560 ( 177)       539 ( 171)       21   17472 (  4992)    832 
```

向打印机发送作业，请暂时等待 Windows 恢复正常，然后记录 Diff 和 Bytes 列的值。

```
Memory:  130480K Avail:   91808K  PageFlts:  1240   InRam Krnl: 2488K P: 7996K
Commit:  30152K Limit: 248432K Peak:  34052K            Pool N: 2224K P: 8012K
Tag  Type        Allocs           Frees           Diff  Bytes          Per Alloc

Drsd Paged       737 (   0)       710 (   0)       27   22464 (     0)    832  
```

如果打印机驱动程序的内存管理工作正常，则在打印后，差异的值应恢复为其原始值21。 但是，正如前面的输出所示，Diff 的值与27的比较，以及与22464的字节数之和。 初始输出与后续输出意味着六个 Drsd 块，总计4992字节，打印期间泄漏。

### <a name="span-idfor_more_informationspanspan-idfor_more_informationspanspan-idfor_more_informationspanfor-more-information"></a><span id="For_More_Information"></span><span id="for_more_information"></span><span id="FOR_MORE_INFORMATION"></span>了解详细信息

如果你认为已识别出泄漏的驱动程序，请参阅[Microsoft 支持](https://support.microsoft.com/)网站并在知识库中搜索相关文章。

### <a name="span-idddk_example_5_monitor_a_terminal_server_session_toolsspanspan-idddk_example_5_monitor_a_terminal_server_session_toolsspanexample-5-monitor-a-terminal-server-session"></a><span id="ddk_example_5_monitor_a_terminal_server_session_tools"></span><span id="DDK_EXAMPLE_5_MONITOR_A_TERMINAL_SERVER_SESSION_TOOLS"></span>示例5：监视终端服务器会话

此示例显示了几种显示终端服务会话池分配的方式。 它演示了如何使用 **/s**命令行参数，以及**s**、 *TSSessionID*和**i**正在运行的参数。

以下命令显示来自所有终端服务会话池的分配。 在此示例中，本地计算机（配置为终端服务器）正在托管会话，客户端计算机正在使用远程桌面功能连接到主机。

```
poolmon /s
```

在响应中，PoolMon 显示来自所有会话池的分配。 请注意标头中的 "所有会话池信息" 标题。

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

若要查看特定会话池的分配，请立即键入 **/s**参数之后的会话 ID，如以下命令中所示。 此命令显示终端服务会话0的会话池分配。

```
poolmon /s0
```

在响应中，PoolMon 显示终端服务会话0的会话池中的分配。 请注意标头中的 "会话0池信息" 标题。

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

若要帮助确定哪些驱动程序和组件正在从会话池中分配内存，请添加 **/g**参数，如以下命令中所示。 **/G**参数添加 \_ 列出了分配每个标记的 Windows 组件和驱动程序的映射驱动程序列。

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

你还可以配置 "终端服务" 会话池显示，而 PoolMon 正在运行。 下表按键入顺序显示了一系列正在运行的命令，以及生成的 PoolMon 显示。

此系列以启动 PoolMon 的命令开头。 所有其他参数都是在 PoolMon 正在运行时键入的。

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
<th align="left">密钥</th>
<th align="left">结果</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>显示所有会话池。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>些</strong></p></td>
<td align="left"><p>显示系统池。</p></td>
<td align="left"><p><strong>S</strong>参数用于切换系统池与终端服务会话池之间的显示。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>显示会话0池。</p></td>
<td align="left"><p>可以在显示系统池的同时键入会话 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>7</strong></p></td>
<td align="left"><p>显示 session 7 池。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>的</strong></p></td>
<td align="left"><p>显示会话7的池分配，按分配数排序。</p></td>
<td align="left"><p>所有标准运行参数对于会话池显示都有效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>显示会话0的分配，按分配数排序。</p></td>
<td align="left"><p>会话和排序选项会一直保留，直到发生更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>些</strong></p></td>
<td align="left"><p>显示系统池。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>些</strong></p></td>
<td align="left"><p>显示会话0的分配，按分配数排序。</p></td>
<td align="left"><p>会话选项已保留。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>10ENTER</strong></p></td>
<td align="left"><p>显示会话1分配，并显示会话0分配。</p></td>
<td align="left"><p>如果<strong>没有，</strong>则只能输入0到9的会话 id。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>提示输入终端服务器会话 ID。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>10</strong></p></td>
<td align="left"><p>显示会话10分配。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>提示输入终端服务器会话 ID。</p></td>
<td align="left"><p>若要显示所有会话池，请按<strong>i</strong> ，然后按 enter。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>回车</strong></p></td>
<td align="left"><p>显示所有会话池。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

只有配置为终端服务器的系统才会从会话池中分配内存。 如果你使用 PoolMon 在不是终端服务器的计算机上显示会话池，或者你键入的会话 ID 在 Windows 上不存在，则 PoolMon 不会显示任何分配。 相反，它只显示具有常规内存数据的标题。

以下命令显示来自所有终端服务会话池的分配：

```
poolmon /s
```

下图显示了向运行 Windows XP 但未能配置为终端服务器的计算机提交了 **/s**命令后会产生的 PoolMon 显示：

```
 Memory:  260620K Avail:   44956K  PageFlts:   308   InRam Krnl: 2744K P:20444K
 Commit: 185452K Limit: 640872K Peak: 192472K            Pool N: 8112K P:20648K
 All sessions pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc
```

 

 





