---
title: 驱动程序验证程序命令语法
description: 在命令提示符窗口中运行验证程序实用工具时，使用以下语法。您可以键入相同的单个行上的多个选项。
ms.assetid: 7cdf5277-7187-4e90-b22a-6f828f06e2fb
keywords:
- 驱动程序验证工具命令语法的驱动程序开发工具
topic_type:
- apiref
api_name:
- Driver Verifier Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11b9b8b31f3e77cf5abd47298c6e627fc7f7b1c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363755"
---
# <a name="driver-verifier-command-syntax"></a>驱动程序验证程序命令语法


在命令提示符窗口中运行验证程序实用工具时，使用以下语法。

您可以键入相同的单个行上的多个选项。 例如：

```
verifier /flags 7 /driver beep.sys flpydisk.sys
```

**Windows 10**

可以使用 **/volatile**一些驱动程序验证程序使用的参数 **/flags**选项且 **/标准**。 不能使用 **/volatile**与 **/flags**选项[DDI 符合性检查](ddi-compliance-checking.md)，[电源框架延迟模糊](concurrency-stress-test.md)， [Storport 验证](dv-storport-verification.md)，或[SCSI 验证](scsi-verification.md)。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

```
  verifier /standard /all
  verifier /standard /driver NAME [NAME ...]
  verifier /flags <options> /all
  verifier /flags <options> /driver NAME [NAME ...]
  verifier /rules [OPTION ...]
  verifier /query
  verifier /querysettings
  verifier /bootmode [persistent | disableafterfail | oneboot]
  verifier /reset
  verifier /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /faultssystematic [OPTION ...] 
  verifier /log LOG_FILE_NAME [/interval SECONDS]
  verifier /volatile /flags <options>
  verifier /volatile /adddriver NAME [NAME ...]
  verifier /volatile /removedriver NAME [NAME ...]
  verifier /volatile /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /domain <types> <options> /driver ... [/logging | /livedump]
  verifier /logging
  verifier /livedump
  verifier /?
  verifier /help
```

**Windows 8.1**

可以使用 **/volatile**一些驱动程序验证程序使用的参数 **/flags**选项且 **/标准**。 不能使用 **/volatile**与 **/flags**选项[DDI 符合性检查](ddi-compliance-checking.md)，[电源框架延迟模糊](concurrency-stress-test.md)， [Storport 验证](dv-storport-verification.md)，或[SCSI 验证](scsi-verification.md)。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

```
  verifier /standard /all
  verifier /standard /driver NAME [NAME ...]
  verifier /flags <options> /all
  verifier /flags <options> /driver NAME [NAME ...]
  verifier /rules [OPTION ...]
  verifier /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /faultssystematic [OPTION ...]  
  verifier /log LOG_FILE_NAME [/interval SECONDS]
  verifier /query
  verifier /querysettings
  verifier /bootmode [persistent | disableafterfail | oneboot]
  verifier /reset
  verifier /volatile /flags <options>
  verifier /volatile /adddriver NAME [NAME ...]
  verifier /volatile /removedriver NAME [NAME ...]
  verifier /volatile /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /?
```

**Windows 8，Windows 7，Windows Vista 语法**

可以使用 **/volatile**一些驱动程序验证程序使用的参数 **/flags**选项且 **/标准**。 不能使用 **/volatile**使用 /flags 选项[DDI 符合性检查](ddi-compliance-checking.md)，[电源框架延迟模糊](concurrency-stress-test.md)， [Storport 验证](dv-storport-verification.md)， [SCSI 验证](scsi-verification.md)或使用 **/磁盘**。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

```
verifier [/volatile] [/standard | /flags Options ] [ /all | /driver DriverList ]
verifier /volatile /faults [Probability PoolTags Applications DelayMins] /driver DriverList
verifier /volatile {/adddriver | /removedriver} DriverList
verifier /reset 
verifier /querysettings 
verifier /query 
verifier /log LogFileName [/interval Seconds] 
verifier /? 
```

**Windows Server 2003 语法**

```
verifier [/disk] [ /standard | /flags Options ] [ /all | /driver DriverList ] 
verifier /volatile /flags VolatileOptions 
verifier /volatile {/adddriver | /removedriver} DriverList
verifier /reset 
verifier /querysettings 
verifier /query 
verifier /log LogFileName [/interval Seconds] 
verifier /? 
```

## <a name="span-idddkverifiercommandlinetoolsspanspan-idddkverifiercommandlinetoolsspanparameters"></a><span id="ddk_verifier_command_line_tools"></span><span id="DDK_VERIFIER_COMMAND_LINE_TOOLS"></span>参数


### <a name="span-idverifiercommandlinesyntaxspanspan-idverifiercommandlinesyntaxspanverifier-command-line-syntax"></a><span id="verifier_command_line_syntax"></span><span id="VERIFIER_COMMAND_LINE_SYNTAX"></span>验证程序命令行语法

<span id="________all______"></span><span id="________ALL______"></span> **/all**   
指示在下一次启动后验证所有已安装的驱动程序的驱动程序验证程序。

<span id="________bootmode_mode______"></span><span id="________BOOTMODE_MODE______"></span> **/bootmode** *mode*   
控制是否在重新启动后启用驱动程序验证程序的设置。 若要设置或更改此选项，必须重新启动计算机。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">启动<em>模式</em></th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="persistent"></span><span id="PERSISTENT"></span><strong>persistent</strong></p></td>
<td align="left"><p>确保驱动程序验证程序设置通过多次重启保留 （保留在效果）。 这是默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="disableafterfail"></span><span id="DISABLEAFTERFAIL"></span><strong>disableafterfail</strong></p></td>
<td align="left"><p>如果 Windows 无法启动，此设置将禁用后续的重新启动驱动程序验证程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="oneboot"></span><span id="ONEBOOT"></span><strong>oneboot</strong></p></td>
<td align="left"><p>仅为在下次计算机启动的时启用驱动程序验证程序设置。 驱动程序验证程序已禁用针对后续的重新启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="resetonunusualshutdown"></span><span id="RESETONUNUSUALSHUTDOWN"></span><strong>resetonunusualshutdown</strong></p></td>
<td align="left"><p>（在 Windows 10，版本 1709年中引入）驱动程序验证程序将一直持续到异常关闭的时间。 其缩写<strong>rous</strong>，可以使用。
</p></td>
</tr>
</tbody>
</table>



<span id="________disk______"></span><span id="________DISK______"></span> **/disk**   
（Windows Server 2003 中引入。 不适用于 Windows 7 和更高版本的 Windows。）激活[磁盘完整性检查](disk-integrity-checking.md)下一次启动后的选项。 不能使用 **/磁盘**与 **/volatile**任何版本的 Windows 上。

<span id="________driver________DriverList______"></span><span id="________driver________driverlist______"></span><span id="________DRIVER________DRIVERLIST______"></span> **/driver** *DriverList*   
指定将验证的一个或多个驱动程序。 *DriverList*是由二进制文件的名称，例如 Driver.sys 驱动程序的列表。 使用空格分隔每个驱动程序名称。 通配符值，例如 n\*.sys，不受支持。

<span id="________driver.exclude________driverlist______"></span><span id="________DRIVER.EXCLUDE________DRIVERLIST______"></span> **/driver.exclude** *DriverList*   
指定将从验证中排除的一个或多个驱动程序。 此参数是仅适用于所有驱动程序选择进行验证。 *DriverList*是由二进制文件的名称，例如 Driver.sys 驱动程序的列表。 使用空格分隔每个驱动程序名称。 通配符值，例如 n\*.sys，不受支持。

<span id="________faults______"></span><span id="________FAULTS______"></span> **/faults**   
(Windows Vista 及更高版本)使驱动程序验证程序中的低资源模拟功能。 可以使用 **/错误**来代替 **/flags 0x4**。 但是，不能使用 **/flags 0x4**与**发生故障/** 子参数。

可以使用的以下子参数均 **/错误**参数，可以配置低资源模拟。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">子参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>概率</em></p></td>
<td align="left"><p>指定驱动程序验证程序将失败的给定的分配的概率。 键入一个数字 （以十进制或十六进制） 来表示在驱动程序验证程序将失败分配 10,000 的机会数。 默认值为 600，表示 600/10000 或 6%。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>池标记</em></p></td>
<td align="left"><p>限制驱动程序验证程序可以分配，则使用指定的池标记为失败的分配。 可以使用通配符字符 (<strong>*</strong>) 来表示池的多个标记。 若要列出多个池标记，请用空格分隔标记。 默认情况下，所有分配可能会都失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Applications</em></p></td>
<td align="left"><p>限制驱动程序验证程序可以故障到指定的程序的分配的分配。 键入可执行文件的名称。 若要列出的程序，单独的程序名称以空格。 默认情况下，所有分配可能会都失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DelayMins</em></p></td>
<td align="left"><p>指定在此期间驱动程序验证程序不会有意失败任何分配的启动后的分钟数。 此延迟使用要加载的驱动程序和系统在测试前达到稳定状态开始。 键入一个数字 （以十进制或十六进制）。 默认值为 7 （分钟）。</p></td>
</tr>
</tbody>
</table>



<span id="_faultssystematic"></span><span id="_FAULTSSYSTEMATIC"></span> **/faultssystematic**  
指定的选项[系统资源不足模拟](systematic-low-resource-simulation.md)。 使用**而 0x40000 可**标志，用于选择系统化低资源模拟选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>enableboottime</p></td>
<td align="left"><p>在计算机重新启动后，启用错误注入。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableboottime</p></td>
<td align="left"><p>禁用错误注入在计算机重新启动后 （这是默认设置）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordboottime</p></td>
<td align="left"><p>启用错误中的注入<em>怎么办</em>模式。 在计算机重启。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetboottime</p></td>
<td align="left"><p>在计算机重新启动后禁用错误注入和清除堆栈的排除列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>enableruntime</p></td>
<td align="left"><p>动态启用故障注入。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableruntime</p></td>
<td align="left"><p>动态禁用错误注入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordruntime</p></td>
<td align="left"><p>启用动态错误中的注入<em>怎么办</em>模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetruntime</p></td>
<td align="left"><p>动态禁用错误注入并清除以前出现故障的堆栈列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>querystatistics</p></td>
<td align="left"><p>显示当前的故障注入统计信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>incrementcounter</p></td>
<td align="left"><p>增量测试通过用于标识时错误被注入的计数器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>getstackid<em>计数器</em></p></td>
<td align="left"><p>检索所指示注入堆栈标识符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>excludestack<em>堆栈 id 为</em></p></td>
<td align="left"><p>排除故障注入堆栈。</p></td>
</tr>
</tbody>
</table>



<span id="________flags________Options______"></span><span id="________flags________options______"></span><span id="________FLAGS________OPTIONS______"></span> **/flags** *选项*   
在下一步的重启后激活指定的选项。 在 Windows 2000 中，此数字必须以十进制格式输入。 以十进制或十六进制在 Windows XP 及更高版本，可以输入此编号 (与**0x**前缀) 格式。 允许使用以下值的组合。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Decimal</th>
<th align="left">十六进制</th>
<th align="left">标准设置</th>
<th align="left">Option</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 （位 0）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊的池</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 （位 1）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">强制 IRQL 检查</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 （位 2）</p></td>
<td align="left"></td>
<td align="left"><p><a href="low-resources-simulation.md" data-raw-source="[Low Resources Simulation](low-resources-simulation.md)">资源不足模拟</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x8 （3 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">跟踪的池</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>0x10 （4 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O 验证</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>0x20 （5 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">发生死锁检测</a>(Windows XP 及更高版本)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>64</p></td>
<td align="left"><p>0x40 （6 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/O 验证</a>(Windows XP 及更高版本) （在 Windows 7 及更高版本，此选项将自动激活时选择的 I/O 验证）</p></td>
</tr>
<tr class="even">
<td align="left"><p>128</p></td>
<td align="left"><p>0x80 （7 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA 验证</a>(Windows XP 及更高版本)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>256</p></td>
<td align="left"><p>0x100 （8 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">安全检查</a>(Windows XP 及更高版本)</p></td>
</tr>
<tr class="even">
<td align="left"><p>512</p></td>
<td align="left"><p>0x200 （9 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="force-pending-i-o-requests.md" data-raw-source="[Force Pending I/O Requests](force-pending-i-o-requests.md)">强制挂起 I/O 请求</a>(Windows Vista 及更高版本)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1024</p></td>
<td align="left"><p>0x400 （10 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="irp-logging.md" data-raw-source="[IRP Logging](irp-logging.md)">日志记录 IRP</a> (Windows Server 2003 及更高版本)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2048</p></td>
<td align="left"><p>0x800 （11 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">杂项检查</a>(Windows Vista 及更高版本)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8192</p></td>
<td align="left"><p>0x2000 （13 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="invariant-mdl-checking-for-stack.md" data-raw-source="[Invariant MDL Checking for Stack](invariant-mdl-checking-for-stack.md)">固定 MDL 堆栈检查</a>（从 Windows 8 开始）</p></td>
</tr>
<tr class="even">
<td align="left"><p>16384</p></td>
<td align="left"><p>0x4000 （14 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="invariant-mdl-checking-for-driver.md" data-raw-source="[Invariant MDL Checking for Driver](invariant-mdl-checking-for-driver.md)">固定 MDL 驱动程序检查</a>（从 Windows 8 开始）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32768</p></td>
<td align="left"><p>0x8000 （第 15 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="concurrency-stress-test.md" data-raw-source="[Power Framework Delay Fuzzing](concurrency-stress-test.md)">电源框架延迟模糊</a>（从 Windows 8 开始）</p></td>
</tr>
<tr class="even">
<td align="left"><p>65536</p></td>
<td align="left"><p>0x10000 （16 位）</p></td>
<td align="left"></td>
<td align="left"><p>检查 （从 Windows 10） 的端口/微型端口接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>131072</p></td>
<td align="left"><p>0x20000 （17 位）</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 符合性检查</a>（从 Windows 8 开始）</p></td>
</tr>
<tr class="even">
<td align="left"><p>262144</p></td>
<td align="left"><p>而 0x40000 可 （18 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="systematic-low-resource-simulation.md" data-raw-source="[Systematic low resources simulation](systematic-low-resource-simulation.md)">系统资源不足模拟</a>（从 Windows 8.1）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>524288</p></td>
<td align="left"><p>0x80000 （19 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="ddi-compliance-checking.md#ddi_compliance_checking_additional" data-raw-source="[DDI compliance checking (additional)](ddi-compliance-checking.md#ddi_compliance_checking_additional)">DDI 符合性检查 （其他）</a> （从 Windows 8.1）</p></td>
</tr>
<tr class="even">
<td align="left"><p>2097152</p></td>
<td align="left"><p>0x200000 （位 21）</p></td>
<td align="left"></td>
<td align="left"><p><a href="ndis-wifi-verification.md" data-raw-source="[NDIS/WIFI verification](ndis-wifi-verification.md)">NDIS/WIFI 验证</a>（从 Windows 8.1）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8388608</p></td>
<td align="left"><p>0x800000 （23 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="kernel-synchronization-delay-fuzzing.md" data-raw-source="[Kernel synchronization delay fuzzing](kernel-synchronization-delay-fuzzing.md)">内核同步延迟模糊</a>（从 Windows 8.1）</p></td>
</tr>
<tr class="even">
<td align="left"><p>16777216</p></td>
<td align="left"><p>0x1000000 （24 位）</p></td>
<td align="left"></td>
<td align="left"><p><a href="vm-switch-verification.md" data-raw-source="[VM switch verification](vm-switch-verification.md)">VM 交换机验证</a>（从 Windows 8.1）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33554432</p></td>
<td align="left"><p>0x2000000 （25 位）</p></td>
<td align="left"></td>
<td align="left"><p>代码完整性检查 （从 Windows 10）</p></td>
</tr>
</tbody>
</table>



此方法不能用于激活的 SCSI 验证或 Storport 验证选项。 有关信息，请参阅[SCSI 验证](scsi-verification.md)并[Storport 验证](dv-storport-verification.md)。

<span id="________flags________VolatileOptions______"></span><span id="________flags________volatileoptions______"></span><span id="________FLAGS________VOLATILEOPTIONS______"></span> **/flags** *VolatileOptions*   
指定立即更改而无需重新启动 Windows 2000，Windows XP 和 Windows Server 2003 中的 Driver Verifier 选项。 (在 Windows Vista 中，可以使用 **/volatile**所有的参数 **/flags**值。)

在 Windows 2000 中，输入十进制格式的数字。 在 Windows XP 和 Windows 2003 中，输入一个数字以十进制或十六进制格式 (与**0x**前缀)。

允许以下值的任意组合。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Decimal</th>
<th align="left">十六进制</th>
<th align="left">Option</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 （位 0）</p></td>
<td align="left"><p>特殊池</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 （位 1）</p></td>
<td align="left"><p>强制 IRQL 检查</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 （位 2）</p></td>
<td align="left"><p>资源不足模拟</p></td>
</tr>
</tbody>
</table>



<span id="________iolevel________Level______"></span><span id="________iolevel________level______"></span><span id="________IOLEVEL________LEVEL______"></span> **/iolevel** *级别*   
(仅适用于 Windows 2000)指定的级别[I/O 验证](i-o-verification.md)。

值*级别*可以是**1**或**2**。 默认值是**1**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">级别值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>1</strong></p></td>
<td align="left"><p>启用级别 1 I/O 验证 （默认值）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2</strong></p></td>
<td align="left"><p>使第 1 级 I/O 验证和级别 2 I/O 验证</p></td>
</tr>
</tbody>
</table>



如果未启用的 I/O 验证 (通过使用 **/flags 0x10**)， **/iolevel**将被忽略。

<span id="________log________LogFileName_______interval_Seconds_______"></span><span id="________log________logfilename_______interval_seconds_______"></span><span id="________LOG________LOGFILENAME_______INTERVAL_SECONDS_______"></span> **/log** *LogFileName* \[ **/interval**|*Seconds*\]   
具有名称创建一个日志文件*LogFileName*。 驱动程序验证程序会定期将写入到此文件的统计信息。 有关详细信息，请参阅[创建日志文件](creating-log-files.md)。

如果**verifier /log**在命令行处键入命令，命令提示符不会返回。 若要关闭日志文件，并返回一条提示，请使用 CTRL + C 键。 在重新启动后，若要创建一个日志，你必须提交**verifier /log**试命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="________interval________Seconds______"></span><span id="________interval________seconds______"></span><span id="________INTERVAL________SECONDS______"></span> <strong>/interval</strong> <em>秒</em></p></td>
<td align="left"><p>指定日志文件更新之间的间隔。 默认值为 30 秒。</p></td>
</tr>
</tbody>
</table>



<span id="_rules_Option"></span><span id="_rules_option"></span><span id="_RULES_OPTION"></span> **/rules** *选项*  
可以禁用 （高级） 的规则的选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>查询</strong></p></td>
<td align="left"><p>显示可控制规则的当前状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>reset</strong></p></td>
<td align="left"><p>将所有规则重都置为其默认状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>默认值</strong> <em>ID</em></p></td>
<td align="left"><p>设置规则<em>ID</em>为其默认状态。 有关受支持的规则，规则<em>ID</em>是<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)"> <strong>Bug 检查 0xC4</strong> </a> (DRIVER_VERIFIER_DETECTED_VIOLATION) 参数 1 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>disable</strong> <em>ID</em></p></td>
<td align="left"><p>禁用指定规则<em>ID</em>。 有关受支持的规则，规则<em>ID</em>是<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)"> <strong>Bug 检查 0xC4</strong> </a> (DRIVER_VERIFIER_DETECTED_VIOLATION) 参数 1 值。</p></td>
</tr>
</tbody>
</table>



<span id="________standard"></span><span id="________STANDARD"></span> **/standard**  
(Windows XP 及更高版本)在下一次启动后将激活"标准"或默认的 Driver Verifier 选项。 Windows XP 中的标准选项[特殊池](special-pool.md)，[强制 IRQL 检查](force-irql-checking.md)，[池跟踪](pool-tracking.md)， [I/O 验证](i-o-verification.md)， [发生死锁检测](deadlock-detection.md)，并[DMA 验证](dma-verification.md)。 这相当于 **/flags 0xBB**。 从 Windows Vista 开始，标准选项还包括[安全检查](security-checks.md)并[杂项检查](miscellaneous-checks.md)。 这相当于 **/flags 0x9BB**。 从 Windows 8 开始，标准选项还包括[DDI 符合性检查](ddi-compliance-checking.md)。 这相当于 **/flags 0x209BB**。

> [!NOTE]
> 从 Windows 10 版本 1803，使用后 **/flags 0x209BB**将不再自动启用 WDF 验证。 使用 **/标准**启用标准选项，使用包含 WDF 验证语法。 请参阅[驱动程序验证工具的命令语法](https://docs.microsoft.com/windows-hardware/drivers/devtest/verifier-command-line)有关详细信息。

<span id="________volatile______"></span><span id="________VOLATILE______"></span> **/volatile**   
更改的设置而无需重启计算机。 易失性的设置将立即生效。

在 Windows Vista 和更高版本的 Windows 上，可以使用 **/volatile**参数与 **/flags**参数来启用和禁用某些选项，而不重新启动。 此外可以使用 **/volatile**与 **/adddriver**并 **/removedriver**参数来启动或停止驱动程序的验证，而无需重新启动，即使驱动程序验证程序尚未运行。

在 Windows Vista 之前的 Windows 版本上 **/volatile**参数可以只用于中列出的选项*VolatileOptions*和可用于启动或停止的驱动程序而无需验证仅当驱动程序验证程序已在运行和重新启动计算机，重新启动操作。

有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="__adddriver_VolatileDriverList"></span><span id="__adddriver_volatiledriverlist"></span><span id="__ADDDRIVER_VOLATILEDRIVERLIST"></span> <strong>/adddriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p>(Windows XP 及更高版本)将指定的驱动程序添加到易失性的设置。 若要指定多个驱动程序，列出它们的名称，由空格分隔。 通配符值，例如 n<em>.sys，不受支持。 请参阅<a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">使用易失性设置</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_removedriver_VolatileDriverList"></span><span id="_removedriver_volatiledriverlist"></span><span id="_REMOVEDRIVER_VOLATILEDRIVERLIST"></span><strong>/removedriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p>(Windows XP 及更高版本)从易失性的设置中移除指定的驱动程序。 若要指定多个驱动程序，列出它们的名称，由空格分隔。 通配符值，例如 n</em>.sys，不受支持。 请参阅<a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">使用易失性设置</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>



<span></span>  

<span id="________reset______"></span><span id="________RESET______"></span> **/reset**   
清除所有驱动程序验证程序设置。 在下一步启动之后，将验证没有驱动程序。

<span id="________querysettings______"></span><span id="________QUERYSETTINGS______"></span> **/querysettings**   
(Windows XP 及更高版本)显示的选项将激活和下一次启动后，将验证的驱动程序的摘要。 显示不包括驱动程序和通过使用添加的选项 **/volatile**参数。 若要查看这些设置的其他方法，请参阅[查看驱动程序验证器设置](viewing-driver-verifier-settings.md)。

<span id="________query______"></span><span id="________QUERY______"></span> **/query**   
显示驱动程序验证程序的当前活动的摘要。 **级别**中显示的字段是使用设置的选项的十六进制值 **/volatile**参数。 请参阅[监视全局计数器](monitoring-global-counters.md)并[监视各个计数器](monitoring-individual-counters.md)有关每个统计信息的说明。

<span id="________domain_Types_Options_______"></span><span id="________domain_types_options_______"></span><span id="________DOMAIN_TYPES_OPTIONS_______"></span> **/domain** *类型* **** *选项*   
控件的验证程序扩展插件设置。 支持以下验证器扩展插件类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>类型</em></th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="wdm"></span><span id="WDM"></span><strong>wdm</strong></p></td>
<td align="left"><p>用于 WDM 驱动程序验证器扩展插件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ndis"></span><span id="NDIS"></span><strong>ndis</strong></p></td>
<td align="left"><p>启用网络驱动程序验证工具扩展。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ks"></span><span id="KS"></span><strong>ks</strong></p></td>
<td align="left"><p>启用内核模式驱动程序流式处理的验证程序扩展。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="audio"></span><span id="AUDIO"></span><strong>audio</strong></p></td>
<td align="left"><p>使音频驱动程序的验证程序扩展。</p></td>
</tr>
</tbody>
</table>



支持以下扩展选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>选项</em></th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="rules.default"></span><span id="RULES.DEFAULT"></span><strong>rules.default</strong></p></td>
<td align="left"><p>启用所选的验证程序扩展插件的默认验证规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="rules.all"></span><span id="RULES.ALL"></span><strong>rules.all</strong></p></td>
<td align="left"><p>启用所选的验证程序扩展的所有验证规则。</p></td>
</tr>
</tbody>
</table>

<span id="________logging_______"></span><span id="________LOGGING_______"></span> **/logging**   
启用日志记录的违反规则检测到的所选的验证程序扩展。

<span id="________livedump_______"></span><span id="________LIVEDUMP_______"></span> **/livedump**   
启用实时违反的规则检测到的所选的验证程序扩展的内存转储收集。

<span id="_______________"></span> **/?**    
显示命令行帮助。

有关使用这些命令的详细信息，请参阅[控制 Driver Verifier](controlling-driver-verifier.md)并[监视 Driver Verifier](monitoring-driver-verifier.md)。

<span id="________help______"></span><span id="________HELP______"></span> **/help**   
显示命令行帮助。

有关使用这些命令的详细信息，请参阅[控制 Driver Verifier](controlling-driver-verifier.md)并[监视 Driver Verifier](monitoring-driver-verifier.md)。

## <a name="span-idreturncodesspanspan-idreturncodesspanspan-idreturncodesspanreturn-codes"></a><span id="Return_Codes"></span><span id="return_codes"></span><span id="RETURN_CODES"></span>返回代码


驱动程序验证程序已运行后，将返回以下值。

|     |                            |
|-----|----------------------------|
| 0   | 退出\_代码\_成功        |
| 1   | 退出\_代码\_错误          |
| 2   | 退出\_代码\_重新启动\_需执行 |











