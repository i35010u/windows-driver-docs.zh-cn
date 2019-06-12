---
title: PoolMon 启动命令
description: 若要启动 PoolMon，请在命令行使用以下语法和参数键入命令。
ms.assetid: 2aa0cf09-f016-46b9-af4e-0f3fbc6fbe5b
keywords:
- PoolMon 启动命令驱动程序开发工具
topic_type:
- apiref
api_name:
- PoolMon Startup Command
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c54fc24ff48c57464085a048da380b8a2afdb7f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327115"
---
# <a name="poolmon-startup-command"></a>PoolMon 启动命令


若要启动 PoolMon，请在命令行使用以下语法和参数键入命令。

```
    poolmon [/iTag] [/xTag] [/c [LocalTagFile]] [/g [PoolTagFile]] [/s[TSSessionID]] [ /p | /p /p ] [/e] [/( | /)]  [/t | /a| /f| /d | /b| /m] [/l] [/n [File]] [/? | /h] 
```

## <a name="span-idddkpoolmonstartupcommandtoolsspanspan-idddkpoolmonstartupcommandtoolsspanparameters"></a><span id="ddk_poolmon_startup_command_tools"></span><span id="DDK_POOLMON_STARTUP_COMMAND_TOOLS"></span>参数


<span id="________i______"></span><span id="________I______"></span> **/i**   
显示仅与指定的池标记的分配。 可以有多个 **/i** PoolMon 命令中的参数。 执行类型之间有空格 **/i**并*标记*参数。

<span id="________x______"></span><span id="________X______"></span> **/x**   
从显示中排除分配，则使用指定的标记。 可以有多个 **/x** PoolMon 命令中的参数。 执行类型之间有空格 **/x**并*标记*参数。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span> *标记*   
指定池标记或池标记模式。 池标记是区分大小写。 *标记*自变量可以包含一个星号 (* *\\* * *) 来表示任何字符或问号的零个或多个实例 (* <em>？</em>*） 来表示任何字符的一个实例。 不以带有星号标记。

<span id="________c______"></span><span id="________C______"></span> **/c**   
将列添加到显示 (映射\_驱动程序) 列出本地计算机上使用每个池标记的驱动程序。 仅在 32 位版本的 Windows 上支持此功能。

<span id="_______LocalTagFile______"></span><span id="_______localtagfile______"></span><span id="_______LOCALTAGFILE______"></span> *LocalTagFile*   
指定本地标记文件，包含本地计算机上的驱动程序的列表的格式化的文本文件和它们所分配的标记值的路径和文件名。 此文件是映射的数据源\_驱动程序将显示当你使用的列 **/c**参数。 默认值为 localtag.txt。

如果您使用 **/c**参数，但未指定的值*LocalTagFile*，和 PoolMon 当前目录中未找到 localtag.txt 文件、 PoolMon 通过扫描生成 localtag.txt 文件在本地计算机上的驱动程序 (%systemroot%\\System32\\驱动程序\\\*.sys)。

<span id="________g______"></span><span id="________G______"></span> **/g**   
将列添加到显示 (映射\_驱动程序) 列出 Windows 组件和常用分配每个标记的驱动程序。

<span id="_______PoolTagFile______"></span><span id="_______pooltagfile______"></span><span id="_______POOLTAGFILE______"></span> *PoolTagFile*   
指定列出 Windows 组件的名称以及常用的驱动程序并将它们分配的标记值的格式化的文本文件路径和文件名。 此文件是映射的数据源\_驱动程序将显示当你使用的列 **/g**参数。

默认值为 pooltag.txt，由 Microsoft 提供的文件。 *Pooltag.txt*工具中包含\\Windows 驱动程序工具包 (WDK) 的其他子目录。

<span id="________s______"></span><span id="________S______"></span> **/s**   
显示从终端服务会话池分配。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span> *TSSessionID*   
显示仅从指定的会话池分配。 执行类型之间有空格 **/s**参数和*TSSessionID*参数。

<span id="________p______"></span><span id="________P______"></span> **/p**   
显示仅从非分页缓冲池分配。

<span id="________p__p_______"></span><span id="________P__P_______"></span> **/p /p**   
显示仅从页面缓冲池分配。

<span id="________e_______"></span><span id="________E_______"></span> **/e**   
显示池总计。 在显示的底部显示总计。

<span id="__________or___"></span><span id="__________OR___"></span> **/(** or **/)**  
打开排序通过更改模式。 与 **/ (** 或 **/)** ，PoolMon 对进行中的值 （分配、 可用操作和字节），此更改而不是值排序。 每个值中的更改显示在括号中的值之后。

使用具有 **/a**， **/f**， **b </b**或者 **/m**。 例如， **poolmon/a**显示按数分配，而**poolmon / (/ a**对显示的分配数的更改进行排序。

左的括号和右括号字符具有相同的效果，并且可以互换使用。

<span id="________t______"></span><span id="________T______"></span> **/t**   
按标记名称按字母顺序排序。 这是默认设置。

<span id="________a______"></span><span id="________A______"></span> **/a**   
对标记排序的分配数。

<span id="________f_______"></span><span id="________F_______"></span> **/f**   
对标记排序可用操作的数目。

<span id="________d______"></span><span id="________D______"></span> **/d**   
对标记排序字节分配和释放的字节数之间的差异。

<span id="________b_______"></span><span id="________B_______"></span> **/b**   
对标记排序使用字节数。

<span id="________m_______"></span><span id="________M_______"></span> **/m**   
对标记排序每个分配的字节数。

<span id="________l______"></span><span id="________L______"></span> **/l**   
将关闭突出显示。 默认情况下，PoolMon 突出显示自上次更新以来已更改的值。

<span id="________n______"></span><span id="________N______"></span> **/n**   
将快照 PoolMon 输出保存到文件，而不是在命令窗口中显示。 可以包含其他命令行参数来配置输出。

快照数据是静态的因为快照文件中不显示在 PoolMon 显示的值中显示此更改的列。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span> *文件*   
指定的名称和快照文件的位置。 默认值为 poolsnap.log。

<span id="__________or__h"></span><span id="__________OR__H"></span> **/?** 或 **/h**  
显示命令行语法。 **/？** 并 **/h**参数具有相同的效果，并且可以互换使用。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

PoolMon 无法生成上的 Windows Server 2003 的 64 位版本的 localtag.txt 文件。 因此， **/c**参数和它的功能是仅在 32 位版本的 Windows 上可用。

可以使用 **/c**并 **/g**同一命令中的参数。 如果这样做，映射\_驱动程序列将显示本地标记和池标记文件中的数据。

此外可以使用 **/c**并 **/g**若要在映射中显示其他文件中的数据\_驱动程序通过指定的文件的列名称和位置与两个参数- **poolmon /c***文件名*或**poolcom /g** *文件名*。 在这种情况下， **/c**并 **/g**参数行为方式相同，并且可以互换使用。

终端服务会话池监视是仅在 Windows Server 2003 和更高版本的 Windows 上可用。

仅当计算机配置为终端服务器时，Win32 子系统的内核模式部分的终端服务会话池中分配的内存。 否则，Windows 池内存用于终端服务从系统池分配。









