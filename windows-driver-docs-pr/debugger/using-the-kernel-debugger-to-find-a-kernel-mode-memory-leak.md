---
title: 使用内核调试程序查找内核模式内存泄漏
description: 使用内核调试程序查找内核模式内存泄漏
ms.assetid: eeadd505-b887-498d-9369-877156526355
keywords:
- 内存泄漏、 内核模式、 内核调试程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5162aa2d79a996f32676e8575a929a2f5aa7d975
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340481"
---
# <a name="using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak"></a>使用内核调试程序查找内核模式内存泄漏


内核调试程序确定内核模式内存泄漏的精确位置。

### <a name="span-idenablepooltaggingwindows2000andwindowsxpspanspan-idenablepooltaggingwindows2000andwindowsxpspanenable-pool-tagging-windows-2000-and-windows-xp"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>启用池标记 （Windows 2000 和 Windows XP）

必须先使用[GFlags](gflags.md)启用池标记。 GFlags 包含在为 Windows 调试工具。 启动 GFlags、 选择**系统注册表**选项卡上，选中**启用池标记**框中，然后依次**应用**。 您必须重新启动 Windows 为此设置，才会生效。

在 Windows Server 2003 和更高版本的 Windows 上，始终启用池标记。

### <a name="span-iddeterminingthepooltagoftheleakspanspan-iddeterminingthepooltagoftheleakspandetermining-the-pool-tag-of-the-leak"></a><span id="determining_the_pool_tag_of_the_leak"></span><span id="DETERMINING_THE_POOL_TAG_OF_THE_LEAK"></span>确定泄漏的池标记

若要确定哪个池标记为泄漏与相关联，它是通常最容易使用 PoolMon 工具执行此步骤。 有关详细信息，请参阅[查找内核模式内存泄漏到使用 PoolMon](using-poolmon-to-find-a-kernel-mode-memory-leak.md)。

或者，可以使用内核调试程序来查找与大型池分配关联的标记。 为此，请按照以下过程：

1.  使用重新加载所有模块[ **.reload （重新都加载模块）** ](-reload--reload-module-.md)命令。

2.  使用[ **！ poolused** ](-poolused.md)扩展。 包括标志"4"的输出进行排序的分页的内存使用：
    ```dbgcmd
    kd> !poolused 4 
    Sorting by Paged Pool Consumed

    Pool Used:
                NonPaged            Paged     
    Tag    Allocs     Used    Allocs     Used 
    Abc         0        0     36405 33930272 
    Tron        0        0       552  7863232 
    IoN7        0        0     10939   998432 
    Gla5        1      128      2222   924352 
    Ggb         0        0        22   828384 
    ```

3.  确定哪个池标记为与最大的内存使用情况相关联。 在此示例中，使用"Abc"的标记的驱动程序使用了最大内存-几乎 34 MB。 因此，是最有可能此驱动程序中为内存泄漏。

### <a name="span-idfindingtheleakspanspan-idfindingtheleakspanfinding-the-leak"></a><span id="finding_the_leak"></span><span id="FINDING_THE_LEAK"></span>查找泄漏

确定池标记后泄漏与相关联，请按照以下过程来查找泄漏本身：

1.  使用[ **ed （输入值）** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令来修改全局系统变量的值**PoolHitTag**。 此全局变量会导致调试器中断时使用的池标记及其值匹配。

2.  设置**PoolHitTag**等于怀疑将成为源的内存泄漏的标记。 应更快的符号解析为指定模块名称"nt"。 （也就是说，向后），必须在 little-endian 格式中输入的标记值。 由于池标记始终为 4 个字符，此标记是实际的-b-c-空间，不只是 A-b 到 c。 因此，使用以下命令：
    ```dbgcmd
    kd> ed nt!poolhittag ' cbA' 
    ```

3.  若要验证的当前值**PoolHitTag**，使用[ **db （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令：
    ```dbgcmd
    kd> db nt!poolhittag L4 
    820f2ba4  41 62 63 20           Abc  
    ```

4.  每次分配或释放与标记该池时，调试器将中断**Abc**。 调试器将中断在这些分配或可用操作，每次使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)调试器命令，以查看堆栈跟踪。

使用此过程，您就可以确定哪些代码驻留在内存中的处于过度分配状态标记具有池**Abc**。

若要清除断点，请设置**PoolHitTag**为零：

```dbgcmd
kd> ed nt!poolhittag 0 
```

如果有多个不同位置分配具有此标记的内存时，以及这些对象位于应用程序或驱动程序已编写的您可以更改源代码即可使用这些分配的每个唯一的标记。

如果您不能重新编译该程序，但你想要确定哪一代码中的几个位置的导致泄漏，可以反汇编每个位置处的代码并使用调试器来编辑驻留在内存中此代码，以便每个实例使用 distinct （和先前未用过） 池标记。 然后允许系统在几分钟的时间或多个运行。 经过一些时间后，再次使用调试器中断并使用[ **！ poolfind** ](-poolfind.md)要查找与每个新标记关联的所有池分配的扩展名。

 

 





