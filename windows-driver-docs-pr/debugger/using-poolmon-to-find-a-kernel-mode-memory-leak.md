---
title: 使用 PoolMon 查找内核模式内存泄漏
description: 使用 PoolMon 查找内核模式内存泄漏
ms.assetid: 383b5d9a-3e99-4dc5-bce9-bd44f2ef1dc0
keywords:
- 内存泄漏，内核模式，PoolMon
- PoolMon
- PoolMon，查找内存泄漏
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ff18c4aacb890050383e581365d24f3d3d9ae2
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802795"
---
# <a name="using-poolmon-to-find-a-kernel-mode-memory-leak"></a>使用 PoolMon 查找内核模式内存泄漏


如果怀疑存在内核模式内存泄漏，确定与该泄漏关联的池标记的最简单方法是使用 PoolMon 工具。

PoolMon ( # A0) 按池标记名称监视池内存使用情况。 此工具包含在 Windows 驱动程序工具包 (WDK) 中。 有关完整说明，请参阅 WDK 文档中的 [PoolMon](https://docs.microsoft.com/windows-hardware/drivers/devtest/poolmon) 。

### <a name="span-idenable_pool_tagging__windows_2000_and_windows_xp_spanspan-idenable_pool_tagging__windows_2000_and_windows_xp_spanenable-pool-tagging-windows-2000-and-windows-xp"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>启用 (Windows 2000 和 Windows XP 的池标记) 

在 Windows 2000 和 Windows XP 上，必须先使用 GFlags 来启用池标记。 GFlags 包含在 Windows 调试工具中。 启动 GFlags，选择 " **系统注册表** " 选项卡，选中 " **启用池标记** " 框，然后选择 " **应用**"。 您必须重新启动 Windows 才能使此设置生效。 有关更多详细信息，请参阅 [GFlags](gflags.md)。

在 Windows Server 2003 和更高版本的 Windows 上，始终启用池标记。

### <a name="span-idusing_poolmonspanspan-idusing_poolmonspanusing-poolmon"></a><span id="using_poolmon"></span><span id="USING_POOLMON"></span>使用 PoolMon

PoolMon 标头显示总页数和非分页池字节数。 列显示每个池标记的池使用情况。 显示将每隔几秒自动更新一次。 例如：

```dbgcmd
Memory: 16224K Avail: 4564K PageFlts: 31 InRam Krnl: 684K P: 680K
Commit: 24140K Limit: 24952K Peak: 24932K Pool N: 744K P: 2180K

## Tag   Type  Allocs       Frees        Diff    Bytes       Per Alloc


CM    Paged   1283  ( 0)  1002  ( 0)   281  1377312   ( 0)  4901
Strg  Paged  10385 ( 10)  6658  ( 4)  3727   317952 ( 512)    85
Fat   Paged   6662  ( 8)  4971  ( 6)  1691   174560 ( 128)   103
MmSt  Paged    614  ( 0)   441  ( 0)   173    83456   ( 0)   482 
```

PoolMon 具有根据各种条件对输出进行排序的命令键。 按下与每个命令相关联的字母，以便对数据重新排序。 每个命令都需要几秒钟的时间。

排序命令包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令键</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>P</strong></p></td>
<td align="left"><p>将显示的标记限制为非分页池、页面缓冲池或两者。 按顺序重复按下每个选项来重复按下 <strong>P</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>按最大字节使用情况对标记排序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>按最大字节分配对标记排序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>按标记名的字母顺序对标记排序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>电邮</strong></p></td>
<td align="left"><p>使显示器在底部包含分页和非分页的总计。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>A</strong></p></td>
<td align="left"><p>按分配大小对标记排序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>果</strong></p></td>
<td align="left"><p>按自由操作对标记排序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>按分配和释放之间的差异对标记排序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>：</strong></p></td>
<td align="left"><p>退出 PoolMon。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idusing_the_poolmon_utility_to_find_a_memory_leakspanspan-idusing_the_poolmon_utility_to_find_a_memory_leakspanusing-the-poolmon-utility-to-find-a-memory-leak"></a><span id="using_the_poolmon_utility_to_find_a_memory_leak"></span><span id="USING_THE_POOLMON_UTILITY_TO_FIND_A_MEMORY_LEAK"></span>使用 PoolMon 实用工具查找内存泄漏

若要查找使用 PoolMon 实用工具的内存泄漏，请遵循以下过程：

1.  开始 PoolMon。

2.  如果确定在非分页池内发生了泄漏，请按 **P** 一次;如果已确定它出现在页面缓冲池中， **请按两** 次。 如果你不知道，请不要按 **P** ，这两种类型的池都包括在内。

3.  按 **B** 按最大字节使用排序显示。

4.  开始测试。 拍摄屏幕截图，并将其复制到记事本。

5.  每半小时拍摄一次新的屏幕快照。 通过比较屏幕截图，确定增加了哪些标记的字节。

6.  停止测试并等待几个小时。 此时间内释放了多少标记？

通常，在应用程序达到稳定运行状态后，它会以大致相同的速率分配内存和释放内存。 如果比释放内存的速度要快得多，则其内存使用将随着时间的推移而增加。 这通常指示内存泄漏。

### <a name="span-idaddressing_the_leakspanspan-idaddressing_the_leakspanaddressing-the-leak"></a><span id="addressing_the_leak"></span><span id="ADDRESSING_THE_LEAK"></span>解决泄漏

确定与该泄漏关联的池标记后，这可能会显示你需要了解的有关泄露的全部信息。 如果需要确定分配例程的哪个特定实例导致了泄漏，请参阅 [使用内核调试器查找内核模式的内存泄漏](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)。

 

 





