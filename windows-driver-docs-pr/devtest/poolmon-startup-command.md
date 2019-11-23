---
title: PoolMon 启动命令
description: 若要启动 PoolMon，请使用以下语法和参数在命令行中键入命令。
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
ms.openlocfilehash: b4c82c4c3d572ce7d5db2c4fa4d0da5936bc4fcb
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038077"
---
# <a name="poolmon-startup-command"></a>PoolMon 启动命令


若要启动 PoolMon，请使用以下语法和参数在命令行中键入命令。

```
    poolmon [/iTag] [/xTag] [/c [LocalTagFile]] [/g [PoolTagFile]] [/s[TSSessionID]] [ /p | /p /p ] [/e] [/( | /)]  [/t | /a| /f| /d | /b| /m] [/l] [/n [File]] [/? | /h] 
```

## <a name="span-idddk_poolmon_startup_command_toolsspanspan-idddk_poolmon_startup_command_toolsspanparameters"></a><span id="ddk_poolmon_startup_command_tools"></span><span id="DDK_POOLMON_STARTUP_COMMAND_TOOLS"></span>Parameters


<span id="________i______"></span><span id="________I______"></span> **/i**   
仅显示具有指定池标记的分配。 在 PoolMon 命令中可以有多个 **/i**参数。 不要在 **/i**和*Tag*参数之间键入空格。

<span id="________x______"></span><span id="________X______"></span> **/x**   
从显示中排除具有指定标记的分配。 在 PoolMon 命令中可以有多个 **/x**参数。 不要键入 **/x**和*Tag*参数之间的空格。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span>*标记*   
指定池标记或池标记模式。 池标记区分大小写。 *标记*参数可以包含星号（ **\*** ）来表示任何字符的零个或多个实例，或包含一个问号（ *<em>？</em>* ）来表示任何字符的一个实例。 不要以星号开始标记。

<span id="________c______"></span><span id="________C______"></span> **/c**   
将列添加到显示（映射\_驱动程序）列出本地计算机上使用每个池标记的驱动程序。 此功能仅在32位版本的 Windows 上受支持。

<span id="_______LocalTagFile______"></span><span id="_______localtagfile______"></span><span id="_______LOCALTAGFILE______"></span>*LocalTagFile*   
指定本地标记文件的路径和文件名、带格式的文本文件（其中包含本地计算机上的驱动程序列表）以及它们分配的标记值。 此文件是在使用 **/c**参数时所显示的映射\_驱动程序列的数据源。 默认值为 localtag。

如果使用 **/c**参数，但未指定*LocalTagFile*的值，并且 poolmon 在当前目录中找不到 Localtag 文件，则 poolmon 会通过扫描本地计算机上的驱动程序（% SystemRoot%\\\\System32\\\*.sys）来生成 localtag 文件。

<span id="________g______"></span><span id="________G______"></span> **/g**   
向显示（映射\_驱动程序）添加一列，其中列出了用于分配每个标记的 Windows 组件和常用的驱动程序。

<span id="_______PoolTagFile______"></span><span id="_______pooltagfile______"></span><span id="_______POOLTAGFILE______"></span>*PoolTagFile*   
指定带格式的文本文件的路径和文件名，该文件列出 Windows 组件的名称以及常用驱动程序的名称和它们分配的标记值。 此文件是在使用 **/g**参数时所显示的映射\_驱动程序列的数据源。

默认值为 pooltag，它是由 Microsoft 提供的文件。 *Pooltag*包含在 Windows 驱动程序工具包（WDK）\\其他子目录的工具中。

<span id="________s______"></span><span id="________S______"></span> **/s**   
显示来自终端服务会话池的分配。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span>*TSSessionID*   
只显示指定会话池中的分配。 不要键入 **/s**参数与*TSSessionID*参数之间的空格。

<span id="________p______"></span><span id="________P______"></span> **/p**   
仅显示非分页池的分配。

<span id="________p__p_______"></span><span id="________P__P_______"></span> **/p/p**   
仅显示分页池的分配。

<span id="________e_______"></span><span id="________E_______"></span> **/e**   
显示池总计。 总计显示在显示的底部。

<span id="__________or___"></span><span id="__________OR___"></span> **/（** 或 **/）**  
打开按更改模式排序。 对于 **/（** 或 **/）** ，PoolMon 按照值（分配、可用操作和字节）中的更改进行排序，而不是按值进行排序。 每个值的更改显示在值后的括号中。

使用 **/a**、 **/f**、 **/b**或 **/m**。 例如， **poolmon/a**按分配数对显示进行排序，而**poolmon/（/a**按分配数量的更改对显示进行排序。

左括号和右括号字符具有相同的效果，并且可以互换使用。

<span id="________t______"></span><span id="________T______"></span> **/t**   
按标记名的字母顺序排序。 这是默认设置。

<span id="________a______"></span><span id="________A______"></span> **/a**   
按分配数对标记排序。

<span id="________f_______"></span><span id="________F_______"></span> **/f**   
按可用操作数对标记排序。

<span id="________d______"></span><span id="________D______"></span> **/d**   
按字节分配和释放的字节数之间的差异对标记排序。

<span id="________b_______"></span><span id="________B_______"></span> **/b**   
按使用的字节对标记排序。

<span id="________m_______"></span><span id="________M_______"></span> **/m**   
按每个分配的字节数对标记排序。

<span id="________l______"></span><span id="________L______"></span> **/l**   
启用突出显示。 默认情况下，PoolMon 会突出显示自上次更新以来发生更改的值。

<span id="________n______"></span><span id="________N______"></span> **/n**   
将 PoolMon 输出的快照保存到文件，而不是将其显示在命令窗口中。 可以包含其他命令行参数来配置输出。

由于快照数据是静态的，因此在 PoolMon 显示中显示值更改的列不会出现在快照文件中。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span>*文件*   
指定快照文件的名称和位置。 默认值为 poolsnap。

<span id="__________or__h"></span><span id="__________OR__H"></span> **/?** 或 **/h**  
显示命令行语法。 **/？** 和 **/h**参数具有相同的效果，并且可以互换使用。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

PoolMon 无法在64位版本的 Windows Server 2003 上生成 localtag 文件。 因此， **/c**参数及其功能仅在32位版本的 Windows 上可用。

可以在同一命令中使用 **/c**和 **/g**参数。 如果执行此操作，映射的\_驱动程序列将显示本地标记和池标记文件中的数据。

你还可以使用 **/c**和 **/G**来显示映射\_驱动程序列中其他文件的数据，方法是使用参数-- **poolmon/c** *filename*或**poolcom/g** *filename*指定文件名和位置。 在这种情况下， **/c**和 **/g**参数的行为相同，并且可以互换使用。

终端服务会话池监视仅在 Windows Server 2003 和更高版本的 Windows 上可用。

仅当计算机配置为终端服务器时，Win32 子系统的内核模式部分才从终端服务会话池中分配内存。 否则，Windows 将从系统池中为终端服务分配池内存。









