---
title: 驱动程序验证程序命令语法
description: 在命令提示符窗口中运行验证程序实用程序时，将使用以下语法。您可以在同一单行上键入几个选项。
ms.assetid: 7cdf5277-7187-4e90-b22a-6f828f06e2fb
keywords:
- 驱动程序验证程序命令语法驱动程序开发工具
topic_type:
- apiref
api_name:
- Driver Verifier Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d47ce504dad6cfcaab7dd3de8fd17435bd886d41
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106454"
---
# <a name="driver-verifier-command-syntax"></a>驱动程序验证程序命令语法


在命令提示符窗口中运行验证程序实用程序时，将使用以下语法。

您可以在同一单行上键入几个选项。 例如：

```
verifier /flags 7 /driver beep.sys flpydisk.sys
```

**Windows 10**

可以将 **/volatile** 参数与一些 Driver Verifier **/flags** 选项和 with **/标准**一起使用。 不能将 **/volatile** 与 **/flags** 选项一起使用，以进行 [DDI 相容性检查](ddi-compliance-checking.md)、 [Power Framework 延迟模糊](concurrency-stress-test.md)处理、 [Storport 验证](dv-storport-verification.md)或 [SCSI 验证](scsi-verification.md)。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

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

可以将 **/volatile** 参数与一些 Driver Verifier **/flags** 选项和 with **/标准**一起使用。 不能将 **/volatile** 与 **/flags** 选项一起使用，以进行 [DDI 相容性检查](ddi-compliance-checking.md)、 [Power Framework 延迟模糊](concurrency-stress-test.md)处理、 [Storport 验证](dv-storport-verification.md)或 [SCSI 验证](scsi-verification.md)。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

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

**Windows 8、Windows 7、Windows Vista 语法**

可以将 **/volatile** 参数与一些 Driver Verifier **/flags** 选项和 with **/标准**一起使用。 不能将 **/volatile** 与/flags 选项配合使用来进行 [DDI 相容性检查](ddi-compliance-checking.md)、 [Power Framework 延迟模糊](concurrency-stress-test.md)处理、 [Storport 验证](dv-storport-verification.md)、 [SCSI 验证](scsi-verification.md) 或使用 **/disk**。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

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

## <a name="span-idddk_verifier_command_line_toolsspanspan-idddk_verifier_command_line_toolsspanparameters"></a><span id="ddk_verifier_command_line_tools"></span><span id="DDK_VERIFIER_COMMAND_LINE_TOOLS"></span>参数


### <a name="span-idverifier_command_line_syntaxspanspan-idverifier_command_line_syntaxspanverifier-command-line-syntax"></a><span id="verifier_command_line_syntax"></span><span id="VERIFIER_COMMAND_LINE_SYNTAX"></span>验证程序命令行语法

<span id="________all______"></span><span id="________ALL______"></span>**/all**   
指示驱动程序验证器在下一次启动之后验证所有已安装的驱动程序。

<span id="________bootmode_mode______"></span><span id="________BOOTMODE_MODE______"></span>**/bootmode** *模式*   
控制在重新启动后是否启用驱动程序验证程序的设置。 若要设置或更改此选项，必须重新启动计算机。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">启动 <em>模式</em></th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="persistent"></span><span id="PERSISTENT"></span><strong>式</strong></p></td>
<td align="left"><p>确保 (在多次重新启动时仍然有效) 驱动程序验证程序设置。 这是默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="disableafterfail"></span><span id="DISABLEAFTERFAIL"></span><strong>disableafterfail</strong></p></td>
<td align="left"><p>如果 Windows 无法启动，则此设置将禁用 Driver Verifier 以便以后重新启动。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="oneboot"></span><span id="ONEBOOT"></span><strong>oneboot</strong></p></td>
<td align="left"><p>仅在计算机下次启动时启用驱动程序验证程序设置。 驱动程序验证程序被禁用，以后重新启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="resetonunusualshutdown"></span><span id="RESETONUNUSUALSHUTDOWN"></span><strong>resetonunusualshutdown</strong></p></td>
<td align="left"><p>Windows 10 中引入的 (，版本 1709) 驱动程序验证程序将一直保留，直到发生异常关闭。 可以使用它的缩写 <strong>"rous"</strong>。
</p></td>
</tr>
</tbody>
</table>



<span id="________disk______"></span><span id="________DISK______"></span>**/disk**   
Windows Server 2003 中引入的 (。 在 windows 7 和更高版本的 Windows 中不可用。 ) 在下一次启动后激活 [磁盘完整性检查](disk-integrity-checking.md) 选项。 不能在任何 Windows 版本上将 **/disk** 与 **/volatile** 一起使用。

<span id="________driver________DriverList______"></span><span id="________driver________driverlist______"></span><span id="________DRIVER________DRIVERLIST______"></span>**/Driver** *DriverList*   
指定要验证的一个或多个驱动程序。 *DriverList* 是按二进制名称列出的驱动程序列表，如 Driver.sys。 使用空格分隔每个驱动程序名称。 不支持通配符值，例如 \* ，sys.databases。

<span id="________driver.exclude________driverlist______"></span><span id="________DRIVER.EXCLUDE________DRIVERLIST______"></span>**/Driver.exclude** *DriverList*   
指定将从验证中排除的一个或多个驱动程序。 仅当选择了所有驱动程序进行验证时，此参数才适用。 *DriverList* 是按二进制名称列出的驱动程序列表，如 Driver.sys。 使用空格分隔每个驱动程序名称。 不支持通配符值，例如 \* ，sys.databases。

<span id="________faults______"></span><span id="________FAULTS______"></span>**/faults**   
 (Windows Vista 和更高版本) 启用驱动程序验证器中的低资源模拟功能。 可以使用 **/faults** 来代替 **/flags 0x4**。 但是，不能将 **/flags 0x4** 与 **/faults** 子参数一起使用。

你可以使用以下子参数的 **/faults** 参数配置低资源模拟。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">子参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>概率</em></p></td>
<td align="left"><p>指定驱动程序验证程序在给定分配中将失败的概率。 键入) 十进制或十六进制形式的数字 (，表示驱动程序验证程序在分配失败的几率（10000）。 默认值600表示600/10000 或6%。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>池标记</em></p></td>
<td align="left"><p>限制驱动程序验证程序无法通过指定的池标记分配的分配数。 您可以使用 (<strong>*</strong>) 通配符来表示多个池标记。 若要列出多个池标记，请用空格分隔标记。 默认情况下，所有分配都可能失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>应用程序</em></p></td>
<td align="left"><p>限制驱动程序验证程序可为指定程序分配的分配数。 键入可执行文件的名称。 若要列出程序，请用空格分隔程序名称。 默认情况下，所有分配都可能失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DelayMins</em></p></td>
<td align="left"><p>指定引导后的分钟数，在此期间，驱动程序验证程序不会有意失败任何分配。 此延迟允许在测试开始之前加载驱动程序并使系统稳定。 以十进制或十六进制) 键入数字 (。 默认值为 7 (分钟) 。</p></td>
</tr>
</tbody>
</table>



<span id="_faultssystematic"></span><span id="_FAULTSSYSTEMATIC"></span>**/faultssystematic**  
指定 [系统低资源模拟](systematic-low-resource-simulation.md)的选项。 使用 **0x40000** 标志选择 "系统低资源" 模拟选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">OPTION</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>enableboottime</p></td>
<td align="left"><p>在计算机重新启动时启用错误注入。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableboottime</p></td>
<td align="left"><p>禁用跨计算机重启的错误注入 (这是默认设置) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordboottime</p></td>
<td align="left"><p>在计算机重新启动 <em>时</em> ，在 "if" 模式下启用错误注入。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetboottime</p></td>
<td align="left"><p>禁用跨计算机重启的错误注入，并清除堆栈排除列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>enableruntime</p></td>
<td align="left"><p>动态启用错误注入。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableruntime</p></td>
<td align="left"><p>动态禁用错误注入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordruntime</p></td>
<td align="left"><p>在 <em>if</em> 模式下动态启用错误注入。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetruntime</p></td>
<td align="left"><p>动态禁用错误注入，并清除以前出错的堆栈列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>querystatistics</p></td>
<td align="left"><p>显示当前错误注入统计信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>incrementcounter</p></td>
<td align="left"><p>递增用于标识注入错误的时间的测试通过计数器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>getstackid <em>计数器</em></p></td>
<td align="left"><p>检索指定的注入堆栈标识符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>excludestack <em>STACKID</em></p></td>
<td align="left"><p>从错误注入中排除堆栈。</p></td>
</tr>
</tbody>
</table>



<span id="________flags________Options______"></span><span id="________flags________options______"></span><span id="________FLAGS________OPTIONS______"></span>**/Flags** *选项*   
在下一次重新启动后激活指定的选项。 在 Windows 2000 中，此数字必须以十进制格式输入。 在 Windows XP 和更高版本中，可以使用十进制或十六进制 (以 **0x** 前缀) 格式输入此数字。 允许使用下列值的任意组合。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">小数</th>
<th align="left">十六进制</th>
<th align="left">标准设置</th>
<th align="left">选项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 (位 0) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 (位 1) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">强制执行 IRQL 检查</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 (位 2) </p></td>
<td align="left"></td>
<td align="left"><p><a href="low-resources-simulation.md" data-raw-source="[Low Resources Simulation](low-resources-simulation.md)">低资源模拟</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x8 (位 3) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">池跟踪</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>0x10 (位 4) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/o 验证</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>0x20 (位 5) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Windows XP 和更高版本 (<a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">死锁检测</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>64</p></td>
<td align="left"><p>0x40 (位 6) </p></td>
<td align="left"></td>
<td align="left"><p> (Windows XP 和更高版本)  (在 Windows 7 和更高版本中<a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/o 验证</a>，则当你选择 "i/o 验证" 时，此选项会自动激活) </p></td>
</tr>
<tr class="even">
<td align="left"><p>128</p></td>
<td align="left"><p>0x80 (位 7) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA 验证</a> (Windows XP 和更高版本) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>256</p></td>
<td align="left"><p>0x100 (位 8) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Windows XP 和更高版本 (<a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">安全检查</a>) </p></td>
</tr>
<tr class="even">
<td align="left"><p>512</p></td>
<td align="left"><p>0x200 (位 9) </p></td>
<td align="left"></td>
<td align="left"><p>在 Windows Vista 和更高版本 (<a href="force-pending-i-o-requests.md" data-raw-source="[Force Pending I/O Requests](force-pending-i-o-requests.md)">强制挂起的 I/o 请求</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>1024</p></td>
<td align="left"><p>0x400 (位 10) </p></td>
<td align="left"></td>
<td align="left"><p> (Windows Server 2003 和更高版本的<a href="irp-logging.md" data-raw-source="[IRP Logging](irp-logging.md)">IRP 日志记录</a>) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2048</p></td>
<td align="left"><p>0x800 (位 11) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p> (Windows Vista 和更高版本的<a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">其他检查</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>8192</p></td>
<td align="left"><p>0x2000 (位 13) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 8 开始<a href="invariant-mdl-checking-for-stack.md" data-raw-source="[Invariant MDL Checking for Stack](invariant-mdl-checking-for-stack.md)">的堆栈 (的固定 MDL 检查</a>) </p></td>
</tr>
<tr class="even">
<td align="left"><p>16384</p></td>
<td align="left"><p>0x4000 (位 14) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 8 开始，<a href="invariant-mdl-checking-for-driver.md" data-raw-source="[Invariant MDL Checking for Driver](invariant-mdl-checking-for-driver.md)">驱动 (的固定 MDL 检查</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>32768</p></td>
<td align="left"><p>0x8000 (位 15) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 8 开始 (的<a href="concurrency-stress-test.md" data-raw-source="[Power Framework Delay Fuzzing](concurrency-stress-test.md)">Power Framework 延迟模糊</a>处理) </p></td>
</tr>
<tr class="even">
<td align="left"><p>65536</p></td>
<td align="left"><p>0x10000 (位 16) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 10 开始 (端口/微型端口接口检查) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>131072</p></td>
<td align="left"><p>0x20000 (位 17) </p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>从 Windows 8 开始 (<a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 相容性检查</a>) </p></td>
</tr>
<tr class="even">
<td align="left"><p>262144</p></td>
<td align="left"><p>0x40000 (位 18) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 8.1 开始 (<a href="systematic-low-resource-simulation.md" data-raw-source="[Systematic low resources simulation](systematic-low-resource-simulation.md)">系统低资源模拟</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>524288</p></td>
<td align="left"><p>0x80000 (位 19) </p></td>
<td align="left"></td>
<td align="left"><p><a href="ddi-compliance-checking.md#ddi_compliance_checking_additional" data-raw-source="[DDI compliance checking (additional)](ddi-compliance-checking.md#ddi_compliance_checking_additional)">DDI 相容性检查) 从 Windows 8.1 开始 (其他 </a> () </p></td>
</tr>
<tr class="even">
<td align="left"><p>2097152</p></td>
<td align="left"><p>0x200000 (位 21) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 8.1 开始 (<a href="ndis-wifi-verification.md" data-raw-source="[NDIS/WIFI verification](ndis-wifi-verification.md)">NDIS/WIFI 验证</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>8388608</p></td>
<td align="left"><p>0x800000 (位 23) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 8.1 开始 (<a href="kernel-synchronization-delay-fuzzing.md" data-raw-source="[Kernel synchronization delay fuzzing](kernel-synchronization-delay-fuzzing.md)">内核同步延迟模糊</a>处理) </p></td>
</tr>
<tr class="even">
<td align="left"><p>16777216</p></td>
<td align="left"><p>0x1000000 (bit 24) </p></td>
<td align="left"></td>
<td align="left"><p><a href="vm-switch-verification.md" data-raw-source="[VM switch verification](vm-switch-verification.md)">VM 交换机验证</a> (从 Windows 8.1 开始) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>33554432</p></td>
<td align="left"><p>0x2000000 (位 25) </p></td>
<td align="left"></td>
<td align="left"><p>从 Windows 10 开始 (代码完整性检查) </p></td>
</tr>
</tbody>
</table>



不能使用此方法激活 SCSI 验证或 Storport 验证选项。 有关信息，请参阅 [SCSI 验证](scsi-verification.md) 和 [Storport 验证](dv-storport-verification.md)。

<span id="________flags________VolatileOptions______"></span><span id="________flags________volatileoptions______"></span><span id="________FLAGS________VOLATILEOPTIONS______"></span>**/Flags** *VolatileOptions*   
指定在 Windows 2000、Windows XP 和 Windows Server 2003 中立即更改的驱动程序验证程序选项，无需重新启动。  (在 Windows Vista 中，可以对所有 **/flags**值使用 **/volatile**参数。 ) 

在 Windows 2000 中，以十进制格式输入数字。 在 Windows XP 和 Windows 2003 中，以十进制或十六进制格式输入数字 (，) 使用 **0x** 前缀。

允许使用下列值的任意组合。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">小数</th>
<th align="left">十六进制</th>
<th align="left">选项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 (位 0) </p></td>
<td align="left"><p>特殊池</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 (位 1) </p></td>
<td align="left"><p>强制 IRQL 检查</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 (位 2) </p></td>
<td align="left"><p>资源不足模拟</p></td>
</tr>
</tbody>
</table>



<span id="________iolevel________Level______"></span><span id="________iolevel________level______"></span><span id="________IOLEVEL________LEVEL______"></span>**/Iolevel** *级别*   
仅 (Windows 2000) 指定 [I/o 验证](i-o-verification.md)的级别。

*Level*的值可以是**1**或**2**。 默认值是 **1**秒。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">级别值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>1</strong></p></td>
<td align="left"><p>启用1级 i/o 验证 (默认值) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2</strong></p></td>
<td align="left"><p>启用1级 i/o 验证和级别 2 i/o 验证</p></td>
</tr>
</tbody>
</table>



如果未使用 **/flags 0x10**) 启用 i/o 验证 (，则将忽略 **/iolevel** 。

<span id="________log________LogFileName_______interval_Seconds_______"></span><span id="________log________logfilename_______interval_seconds_______"></span><span id="________LOG________LOGFILENAME_______INTERVAL_SECONDS_______"></span>**/log** *LogFileName* \[ **/interval** | *秒*\]   
创建名为 *LogFileName*的日志文件。 驱动程序验证程序定期将统计信息写入此文件。 有关详细信息，请参阅 [创建日志文件](creating-log-files.md)。

如果在命令行中键入了 **验证程序/log** 命令，则命令提示符不会返回。 若要关闭日志文件并返回提示，请使用 CTRL + C 键。 重新启动后，若要创建日志，必须再次提交 **验证程序/log** 命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="________interval________Seconds______"></span><span id="________interval________seconds______"></span><span id="________INTERVAL________SECONDS______"></span><strong>/Interval</strong> <em>秒</em></p></td>
<td align="left"><p>指定日志文件更新之间的时间间隔。 默认为 30 秒。</p></td>
</tr>
</tbody>
</table>



<span id="_rules_Option"></span><span id="_rules_option"></span><span id="_RULES_OPTION"></span>**/Rules** *选项*  
可在高级)  (禁用的规则的选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>query</strong></p></td>
<td align="left"><p>显示可控规则的当前状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>reset</strong></p></td>
<td align="left"><p>将所有规则重置为其默认状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>默认</strong> <em>ID</em></p></td>
<td align="left"><p>将规则 <em>ID</em> 设置为其默认状态。 对于支持的规则，规则 <em>ID</em> 为 <a href="/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)"><strong>Bug 检查 0xC4</strong></a> (DRIVER_VERIFIER_DETECTED_VIOLATION) 参数1值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>禁用</strong> <em>ID</em></p></td>
<td align="left"><p>禁用指定的规则 <em>ID</em>。 对于支持的规则，规则 <em>ID</em> 为 <a href="/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)"><strong>Bug 检查 0xC4</strong></a> (DRIVER_VERIFIER_DETECTED_VIOLATION) 参数1值。</p></td>
</tr>
</tbody>
</table>



<span id="________standard"></span><span id="________STANDARD"></span>**/标准**  
 (Windows XP 和更高版本) 会在下一次启动之后激活 "标准" 或默认的驱动程序验证程序选项。 Windows XP 中的标准选项是 [特殊的池](special-pool.md)， [强制执行 IRQL 检查](force-irql-checking.md)， [池跟踪](pool-tracking.md)， [I/o 验证](i-o-verification.md)， [死锁检测](deadlock-detection.md)和 [DMA 验证](dma-verification.md)。 这等效于 **/Flags 0xBB**。 从 Windows Vista 开始，标准选项还包括 [安全检查](security-checks.md) 和 [其他检查](miscellaneous-checks.md)。 这等效于 **/Flags 0x9BB**。 从 Windows 8 开始，标准选项还包括 [DDI 相容性检查](ddi-compliance-checking.md)。 这等效于 **/Flags 0x209BB**。

> [!NOTE]
> 从1803后的 Windows 10 版本开始，使用 **/Flags 0x209BB** 将不再自动启用 WDF 验证。 使用 **/标准** 语法启用标准选项，其中包含 WDF 验证。 有关详细信息，请参阅 [驱动程序验证程序命令语法]() 。

<span id="________volatile______"></span><span id="________VOLATILE______"></span>**/volatile**   
更改设置，无需重新启动计算机。 可变设置将立即生效。

在 Windows Vista 和更高版本的 Windows 上，可以将 **/volatile** 参数与 **/flags** 参数一起使用，以启用和禁用某些选项而无需重新启动。 你还可以将 **/volatile** 与 **/adddriver** 和 **/removedriver** 参数一起使用，以便在不重新启动的情况下启动或停止对驱动程序的验证，即使驱动程序验证器尚未运行也是如此。

在 Windows Vista 之前的 Windows 版本中，只能将 **/volatile** 参数与 *VolatileOptions* 中列出的选项一起使用，并且仅当驱动程序验证程序已在运行并重新启动计算机时，它才可用于启动或停止验证驱动程序，而无需重新启动。

有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="__adddriver_VolatileDriverList"></span><span id="__adddriver_volatiledriverlist"></span><span id="__ADDDRIVER_VOLATILEDRIVERLIST"></span><strong>/Adddriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p> (Windows XP 和更高版本) 将指定的驱动程序添加到可变设置。 若要指定多个驱动程序，请列出它们的名称，用空格分隔。 不支持通配符值，例如 <em> ，sys.databases。 有关详细信息，请参阅 <a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">使用可变设置</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_removedriver_VolatileDriverList"></span><span id="_removedriver_volatiledriverlist"></span><span id="_REMOVEDRIVER_VOLATILEDRIVERLIST"></span><strong>/Removedriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p> (Windows XP 及更高版本) 从可变设置中删除指定的驱动程序。 若要指定多个驱动程序，请列出它们的名称，用空格分隔。 不支持通配符值，例如 </em> ，sys.databases。 有关详细信息，请参阅 <a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">使用可变设置</a> 。</p></td>
</tr>
</tbody>
</table>



<span></span>  

<span id="________reset______"></span><span id="________RESET______"></span>**/reset**   
清除所有驱动程序验证程序设置。 下一次启动后，将不会验证任何驱动程序。

<span id="________querysettings______"></span><span id="________QUERYSETTINGS______"></span>**/querysettings**   
 (Windows XP 和更高版本的) 显示将被激活的选项的摘要，以及下次启动后将验证的驱动程序。 显示不包括使用 **/volatile** 参数添加的驱动程序和选项。 有关查看这些设置的其他方式，请参阅 [查看驱动程序验证程序设置](viewing-driver-verifier-settings.md)。

<span id="________query______"></span><span id="________QUERY______"></span>**/query**   
显示驱动程序验证程序的当前活动的摘要。 显示中的 " **级别** " 字段是用 **/volatile** 参数设置的选项的十六进制值。 有关每个统计信息的说明，请参阅 [监视全局计数器](monitoring-global-counters.md) 和 [监视各个计数器](monitoring-individual-counters.md) 。

<span id="________domain_Types_Options_______"></span><span id="________domain_types_options_______"></span><span id="________DOMAIN_TYPES_OPTIONS_______"></span>**/domain** *类型*  ****  *选项*   
控制验证程序扩展设置。 支持以下验证程序扩展类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>类型</em></th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="wdm"></span><span id="WDM"></span><strong>wdm</strong></p></td>
<td align="left"><p>为 WDM 驱动程序启用验证程序扩展。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ndis"></span><span id="NDIS"></span><strong>以此</strong></p></td>
<td align="left"><p>为网络驱动程序启用验证程序扩展。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ks"></span><span id="KS"></span><strong>ks</strong></p></td>
<td align="left"><p>为内核模式流式处理驱动程序启用验证程序扩展。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="audio"></span><span id="AUDIO"></span><strong>声卡</strong></p></td>
<td align="left"><p>启用音频驱动程序的验证程序扩展。</p></td>
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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="rules.default"></span><span id="RULES.DEFAULT"></span><strong>规则。默认值</strong></p></td>
<td align="left"><p>为所选的验证程序扩展启用默认验证规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="rules.all"></span><span id="RULES.ALL"></span><strong>规则。所有</strong></p></td>
<td align="left"><p>启用所选验证程序扩展的所有验证规则。</p></td>
</tr>
</tbody>
</table>

<span id="________logging_______"></span><span id="________LOGGING_______"></span>**/logging**   
启用所选验证程序扩展检测到的违反规则的日志记录。

<span id="________livedump_______"></span><span id="________LIVEDUMP_______"></span>**/livedump**   
为所选验证程序扩展检测到的冲突规则启用实时内存转储收集。

<span id="_______________"></span> **/?**   
显示命令行帮助。

有关使用这些命令的详细信息，请参阅 [控制驱动程序验证](controlling-driver-verifier.md) 程序和 [监视驱动程序验证程序](monitoring-driver-verifier.md)。

<span id="________help______"></span><span id="________HELP______"></span>**/help**   
显示命令行帮助。

有关使用这些命令的详细信息，请参阅 [控制驱动程序验证](controlling-driver-verifier.md) 程序和 [监视驱动程序验证程序](monitoring-driver-verifier.md)。

## <a name="span-idreturn_codesspanspan-idreturn_codesspanspan-idreturn_codesspanreturn-codes"></a><span id="Return_Codes"></span><span id="return_codes"></span><span id="RETURN_CODES"></span>返回代码


运行驱动程序验证程序后，将返回以下值。

**0**：退出 \_ 代码 \_ 成功

**1**：退出 \_ 代码 \_ 错误

**2**： \_ 需要退出代码 \_ 重新启动 \_