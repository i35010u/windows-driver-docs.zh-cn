---
title: INF LogConfig 指令
description: LogConfig 指令引用一个或多个 INF 编写器定义的部分，其中每个指定的硬件资源的逻辑配置。
ms.assetid: 6b60c3eb-bf70-42f7-bed7-a856fd626d8c
keywords:
- INF LogConfig 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF LogConfig Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76b4fddfb7ba74d4a9784cdafd54d15f32bfbb67
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350390"
---
# <a name="inf-logconfig-directive"></a>INF LogConfig 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**LogConfig**指令引用一个或多个 INF 编写器定义的部分，其中每个指定的硬件资源 − 逻辑配置中断请求行，可以是内存范围、 I/O 端口和 DMA 频道由设备使用。 每个*日志配置部分*指定另一组可由设备的总线相对硬件资源。

```ini
[DDInstall] | 
[DDInstall.LogConfigOverride] 
  
LogConfig=log-config-section[,log-config-section]...
```

适用于非 PnP 设备 INF 文件使用此指令来创建基本配置。

即插即用设备的 INF 文件使用此指令只是为了创建重写配置。

每个命名部分引用的**LogConfig**指令具有以下形式：

```ini
[log-config-section]
 
ConfigPriority=priority-value[,config-type]
[DMAConfig=[DMAattrs:]DMANum[,DMANum]...]
[IOConfig=io-range[,io-range]...]
[MemConfig=mem-range[,mem-range]...]
[IRQConfig=[IRQattrs:]IRQNum[,IRQNum]...]
[PcCardConfig=ConfigIndex[:[MemoryCardBase1][:MemoryCardBase2]][(attrs)]]
[MfCardConfig=ConfigRegBase:ConfigOptions[:IoResourceIndex][(attrs)]...]
...
```

## <a name="entries"></a>条目


<a href="" id="configpriority-priority-value"></a>**ConfigPriority=**<em>priority-value</em>  
对于此逻辑的配置，优先级值指定为以下值之一：

<a href="" id="desired"></a>所需的  
软件配置，最大程度优化。

<a href="" id="normal"></a>正常  
软配置的非最佳比所需。 这是典型的设置。

如果应指定 NORMAL*日志配置节*中定义[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)部分中，但没有*配置类型*可以指定值。

<a href="" id="suboptimal"></a>非最优  
软配置的非最佳比正常。

<a href="" id="hardreconfig"></a>HARDRECONFIG  
需要跳线更改来重新配置。

<a href="" id="hardwired"></a>硬编码  
不能更改。

<a href="" id="restart"></a>重新启动  
需要重启才能生效。

<a href="" id="reboot"></a>重新启动  
这是重新启动的相同。

<a href="" id="poweroff"></a>关闭  
需要电源周期才会生效。

<a href="" id="disabled"></a>已禁用  
硬件/设备已被禁用。

<a href="" id="dmaconfig--dmaattrs--dmanum--dmanum-----"></a>**DMAConfig =**\[*DMAattrs:*\]*DMANum*\[<strong>，</strong>DMANum\]...\]  
*DMAattrs*是可选的如果具有唯一的 8 位 DMA 通道的总线上连接设备和设备使用标准系统 DMA。 否则，它可以是以下字母之一：

| 字母 | 含义    |
|--------|------------|
| **D**  | 32 位 DMA |
| **W**  | 16 位 DMA |
| **N**  | 8 位 DMA  |

 

如果设备使用总线 master DMA，则必须使用**M**以下 （互斥） 字母，该值指示使用 DMA 通道的类型之一：**一个**， **B**，或**F**。如果既没有**A**， **B**，或**F**都指定，则假定标准 DMA 通道。

*DMANum*指定为十进制数字，每个由逗号 （，） 与下一个分隔的一个或多个总线相对 DMA 通道。

<a href="" id="ioconfig-io-range--io-range----"></a>**IOConfig =**<em>io 范围</em>\[**，**<em>io 范围</em>\]...  
指定一个或多个 I/O 端口范围为该设备的以下形式之一：

<a href="" id="start-end---decode-mask---alias-offset---attr------type-1-i-o-range-"></a>*开始结束*\[**(**\[*解码掩码*\]\[*： 别名偏移量*\]\[ *: attr*\]**)** \] （类型 1 I/O 范围）  

<a href="" id="start"></a>*start*  
作为 64 位十六进制地址指定 I/O 端口范围的起始地址。

<a href="" id="end"></a>*end*  
也可用作 64 位十六进制地址指定 I/O 端口范围的结束地址。

<a href="" id="decode-mask"></a>*decode-mask*  
定义别名类型，并且可以为以下任何：

| 掩码值 | 含义         | IOR_Alias 值 |
|------------|-----------------|------------------|
| **3ff**    | 10 位解码   | 0x04             |
| **fff**    | 12 位解码   | 0x10             |
| **ffff**   | 16 位解码   | 0x00             |
| **0**      | 正解码 | 0xFF             |

 

<a href="" id="alias-offset-"></a>*alias-offset*   
不使用。

<a href="" id="attr"></a>*attr*  
指定以字母**M**如果给定的范围是在系统内存中。 如果省略，给定的范围处于 I/O 端口空间。

<a href="" id="size-min-max--align-mask----decode-mask---alias-offset---attr------type-2-i-o-range-"></a><em>大小</em>**@**<em>小-最大</em>\[**%**<em>对齐掩码</em>\] \[ **(**\[*解码掩码*\]\[**:**<em>别名偏移量</em>\] \[ **:**<em>attr</em>\])\] （类型 2 I/O 范围）  

<a href="" id="size"></a>*size*  
指定所需的 I/O 端口范围为 32 位十六进制值的字节数。

<a href="" id="min"></a>*min*  
作为 64 位十六进制地址指定 I/O 端口范围的最低可能起始地址。

<a href="" id="max"></a>*max*  
指定作为 64 位十六进制地址的 I/O 端口范围的结束地址的最大可能。

<a href="" id="align-mask"></a>*对齐掩码*  
按位运算中，若要对齐的整数 （通常，32 位或 64 位） 地址边界上启动 I/O 端口范围 （可选） 指定使用 64-位掩码。

<a href="" id="decode-mask"></a>*decode-mask*  
定义别名类型，并且可以为以下任何：

| 掩码值 | 含义         | IOR_Alias 值 |
|------------|-----------------|------------------|
| **3ff**    | 10 位解码   | 0x04             |
| **fff**    | 12 位解码   | 0x10             |
| **ffff**   | 16 位解码   | 0x00             |
| **0**      | 正解码 | 0xFF             |

 

<a href="" id="alias-offset-"></a>*alias-offset*   
不使用。

<a href="" id="attr"></a>*attr*  
指定以字母**M**如果给定的范围是在系统内存中。 如果省略，给定的范围处于 I/O 端口空间。

<a href="" id="memconfig-mem-range--mem-range----"></a>**MemConfig=**<em>mem-range</em>\[**,**<em>mem-range</em>\]...  
指定一个或多个设备的内存范围的以下形式之一：

```ini
start-end[(attr)] | size@min-max[%align-mask][(attr)]
```

<a href="" id="start"></a>*start*  
指定设备的内存范围的起始 （总线相对） 物理地址为 64 位十六进制值。

<a href="" id="end"></a>*end*  
也可用作 64 位十六进制值指定内存范围结束的物理的地址。

<a href="" id="attr"></a>*attr*  
指定为一个或多个以下字母的内存范围的属性：

| 字母 | 含义                                             |
|--------|-----------------------------------------------------|
| **R**  | 只读                                           |
| **W**  | 只写                                          |
| **RW** | 读取/写入                                          |
| **C**  | 允许的组合的写入                              |
| **H**  | 可缓存                                           |
| **F**  | Prefetchable                                        |
| **D**  | 卡解码寻址为 32 位，而不是 24 位 |

 

如果这两个**R**并**W**指定或如果属性均未指定，则假定为读/写。

<a href="" id="size-"></a>*size*   
指定所需的内存范围为 32 位十六进制值中的字节数。

<a href="" id="min--"></a>*min*   
为 64 位十六进制值指定可能的最低起始地址的设备的内存范围。

<a href="" id="max"></a>*max*  
指定为 64 位十六进制值的内存范围的结束地址的最大可能。

<a href="" id="align-mask-"></a>*对齐掩码*   
按位运算中，若要对齐的整数 （通常是 64 位） 地址边界上启动设备的内存范围 （可选） 指定使用 64-位掩码。

如果省略对齐掩码，则默认的内存对齐方式是在 4k 边界 (FFFFF000)。

<a href="" id="irqconfig--irqattrs--irqnum--irqnum----"></a>**IRQConfig =**\[*IRQattrs:*\]*IRQNum*\[**，**<em>IRQNum</em>\]...  
*IRQattrs*如果设备使用总线相对，边缘触发 IRQ 省略。 否则，指定**L**以指示级别触发 IRQ 和**LS**如果设备可以共享此项中列出的 IRQ 行。

*IRQNum*指定一个或多个设备可以使用以十进制数的总线相对 Irq，每个以逗号 （，） 分隔从下一步。

<a href="" id="pccardconfig-configindex---memorycardbase1---memorycardbase2----attrs--"></a>**PcCardConfig=**<em>ConfigIndex</em>\[**:**\[*MemoryCardBase1*\]\[**:**<em>MemoryCardBase2</em>\]\]\[**(**<em>attrs</em>**)**\]  
配置 CardBus 寄存器和/或创建最多两个永久内存窗口可映射到设备的属性空间。 驱动程序可以使用内存窗口从 ISR.访问属性空间 以十六进制格式指定所有数值。

元素**PcCardConfig**条目如下所示：

<a href="" id="configindex"></a>*ConfigIndex*  
PCMCIA 总线上指定设备的 8 位 PCMCIA 配置索引。

<a href="" id="memorycardbase1"></a>*MemoryCardBase1*  
（可选） 指定第一个内存窗口的 32 位基址。

<a href="" id="memorycardbase2"></a>*MemoryCardBase2*  
（可选） 指定第二个内存窗口的 32 位基址。

<a href="" id="attrs"></a>*attrs*  
（可选） 指定一个或多个设备，由空格分隔的属性。 无效的属性说明符使整个**PcCardConfig**条目。 如果提供多个特定属性说明符，则属性应用于单个 I/O 或内存 windows 设备。 如果只提供一个说明符，该属性将被应用于所有窗口 （请参阅下面的示例）。

具体而言，如果提供了多个说明符，第一个说明符找到从左到右读取将应用于第一个窗口，并应用于第二个窗口的下一步说明符。 最多两个 I/O 窗口，这两个内存窗口可能会控制由单个**PcCardConfig**条目。 如果设备具有两个以上内存窗口，则第二个**PcCardConfig**条目必须包含。

属性包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>W</strong></td>
<td align="left"><p>16 位 I/O 数据路径。</p>
<p>默认值是 8 位如果指定了 INF <strong>LogConfig</strong>指令。 如果没有<strong>LogConfig</strong>指定指令，该驱动程序将使用 16 位 I/O。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S</strong><em>n</em></td>
<td align="left"><p>~ IOCS16 源。</p>
<p>如果<em>n</em>为 0，~ IOCS16 基于 datasize 位的值。 如果 n 为 1，~ IOCS16 基于 ~ IOIS16 信号从设备。 默认值是<strong>S</strong>1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Z</strong><em>n</em></td>
<td align="left"><p>I/O 8 位，零个等待状态。</p>
<p>如果<em>n</em>是 1，8 位 I/O 访问，则出现与零个额外的等待状态。 如果<em>n</em>为 0，具有额外的等待状态进行访问。 此标志没有任何意义的 16 位 I/O。 默认值是<strong>Z</strong>0.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Xl</strong><em>n</em></td>
<td align="left"><p>I/O 等待状态。</p>
<p>如果 n 为 1，16 位系统访问发生与一个额外的等待状态。 默认值是<strong>Xl</strong>1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>M</strong></td>
<td align="left">16 位内存数据路径。 默认值为 8 位。</td>
</tr>
<tr class="even">
<td align="left"><strong>M8</strong></td>
<td align="left">8 位内存数据路径。</td>
</tr>
<tr class="odd">
<td align="left"><strong>XM</strong><em>n</em></td>
<td align="left"><p>内存等待的状态，其中 n 可以是 0、 1、 2 或 3。</p>
<p>此值确定 16 位内存窗口访问的额外的等待状态的数。 默认值是<strong>XM</strong>3.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>A</strong></td>
<td align="left">要映射为属性内存的内存范围。</td>
</tr>
<tr class="odd">
<td align="left"><strong>C</strong></td>
<td align="left">要映射为常见的内存 （默认值） 的内存范围。</td>
</tr>
</tbody>
</table>

 

例如，(WB CA M XM1 XI0) attrs 值会转换为以下：

第一个 I/O 窗口是 16 位

第二个 I/O 窗口 8 位

第一个内存窗口很常见

第二个内存窗口是属性

内存是 16 位

在内存窗口上的一个等待状态

零等待 I/O 在 windows 上的状态

<a href="" id="mfcardconfig-configregbase-configoptions--ioresourceindex---attrs-----"></a>**MfCardConfig=**<em>ConfigRegBase</em>**:**<em>ConfigOptions</em>\[**:**<em>IoResourceIndex</em>\]\[**(**<em>attrs</em>**)**\]...指定的配置集的特性内存位置注册的多功能设备的一个函数，如下所示：

<a href="" id="configregbase"></a>*ConfigRegBase*  
指定此函数的多功能设备的配置寄存器的属性偏移量。

<a href="" id="configoptions-"></a>*ConfigOptions*   
指定的 8 位 PCMCIA 配置选项寄存器。

<a href="" id="ioresourceindex-"></a>*IoResourceIndex*   
指定的索引**IOConfig**总线驱动程序，以使用编程配置基本的 I/O 并限制寄存器的条目。 此索引是从零开始，零，即指定初始**IOConfig**在此条目*日志配置部分*。

<a href="" id="attrs-"></a>*attrs*   
如果设置为字母**A**，将定向 PCMCIA 总线驱动程序以打开配置和状态寄存器中的音频启用。

每个**MfCardConfig**条目提供有关单个函数的多功能设备的信息。 当一组**LogConfig**每个指令引用离散*日志配置节*INF 中[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)部分中，每个*日志配置节*必须具有其条目，其中包括**MfCardConfig**中相同的顺序列出的条目。

<a name="remarks"></a>备注
-------

一个**LogConfig**可以在任何每个的制造商，每个模型指定指令[ **INF *DDInstall*部分**](inf-ddinstall-section.md)或[ **INF *DDInstall*。LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)。

通常支持几种备用逻辑配置的非 PnP 设备 INF 定义一组*日志配置部分*下*DDInstall*部分。 每个*日志配置部分*指定一组离散的逻辑配置资源。 它还包括**ConfigPriority**条目，对每个逻辑配置根据及其对设备和驱动程序性能的影响进行排名，简化的初始化，等等。

对于即插即用设备，即插即用管理器将一组逻辑硬件资源分配给每个即插即用设备。 PnP 管理器，即查询系统总线驱动程序、 接收其报表的每个设备 I/O 总线配置资源在使用中，并分配逻辑硬件资源，以实现最佳的系统级均衡所有此类资源的使用情况中的每个设备设置.

因此， **LogConfig**指令下*DDInstall*部分忽略的即插即用设备。 若要重写报告的即插即用设备的总线的资源，包括**LogConfig**指令下[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)部分。 在这种情况下，在指定的资源*日志配置部分*而不是报告的总线。

平台扩展可以添加到*DDInstall*节，其中包含**LogConfig**指令，或设置为[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)部分，若要指定特定于平台的或特定于操作系统的逻辑配置。 有关详细信息，请参阅[创建一个 INF 文件](overview-of-inf-files.md)。

给定*日志配置节*名称必须是唯一的 INF 文件，但它可以被**LogConfig**指令在其他 INF *DDInstall*相同的设备的部分. 每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

只有一个**ConfigPriority**条目可在每个*日志配置部分*。 可以有多个各项之一的其他条目，具体取决于设备的硬件资源要求。

一个或多个**MfCardConfig =** 条目仅出现在*日志配置节*引用**LogConfig**指令<em>DDInstall</em>**.LogConfigOverride**的多功能设备 INF 部分。 多功能设备的 INF 文件有关的详细信息，请参阅[支持多功能设备](https://msdn.microsoft.com/library/windows/hardware/ff542743)。

### <a name="logconfig-referenced-section-entries-and-values"></a>LogConfig 引用节条目和值

从*日志配置部分*，系统安装程序生成二进制逻辑配置记录并将它们存储在注册表中。

INF 文件可以包含任意数量的每个设备*日志配置部分*。 但是，每个此类部分必须包含安装一台设备的完整信息。 INF 一般情况下，应指定的条目中的每个其*日志配置部分*顺序相同。 INF 应指定项按最佳顺序如何驱动程序初始化其设备适合每个组。

如果多个*日志配置部分*给定的设备，这些 INF 部分只有一个则在安装过程中使用的是存在。 此类 INF 部分文件控制此类的部分通过使用该**ConfigPriority**值，它在每个此类中提供该值*日志配置部分*。 也就是说，系统安装程序尝试采用 INF 文件中的所有配置优先级，但如果找到与已安装的设备发生冲突，则可能会选择较低的排名逻辑配置。

在安装期间，从每个项目中的一个且只有一个资源给定*日志配置部分*选择并将其分配给特定设备。 如果特定的设备需要多个相同类型的资源，必须在使用该类型的条目一组其*日志配置部分*。

例如，若要确保两个 I/O 端口范围为特定的设备，两个**IOConfig =** 中，必须指定条目*日志配置部分*为该设备。 但是，如果设备需要没有 IRQ，可以省略其 INF **IRQConfig**中的条目*日志配置部分*。

<a name="examples"></a>示例
--------

此示例显示了一些有效**PcCardConfig** PCMCIA 设备的条目。

```ini
PcCardConfig=0:E0000:F0000(W)
PcCardConfig=0:E0000(M)
PcCardConfig=0::(W)
PcCardConfig=0(W)
```

此示例演示中的类型 1 I/O 范围规范**IOConfig**条目。 它指定的 I/O 端口区域的大小，可以开始在 1F8、 2F8 或 3F8 8 个字节。

```ini
IOConfig=1F8-1FF, 2F8-2FF, 3F8-3FF
```

与此相反，此示例演示中的类型 2 I/O 范围规范**IOConfig**条目。 它指定的 I/O 端口区域的大小，可以从开始 300、 308、 310、 318，320 或 328 的八个字节。

```ini
IOConfig=8@300-32F%FF8
```

此示例显示了一套**IOConfig**四个端口设备的条目，每个指定 I/O 端口由与下一个 0x400 字节偏移量的范围。

```ini
IoConfig=0x200-0x21f
IoConfig=0x600-0x61f
IoConfig=0xA00-0xA1f
IoConfig=0xE00-0xE1f
```

接下来两个示例演示典型**MemConfig**条目。

此示例指定可以从开始 C0000 或 D0000 32 kb 的内存区域。

```ini
MemConfig=C0000-C7FFF, D0000-D7FFF
```

此示例指定在 64k 边界上启动 32 k 个字节的内存区域。

```ini
MemConfig=8000@C0000-D7FFF%F0000
```

此示例演示如何系统 HDC 类 INF 文件设置了几项*日志配置部分*泛型 ESDI 硬盘控制器和使用[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)部分，了解特定的 IDE 控制器。

```ini
[MS_HDC] ; per-manufacturer Models section
%FujitsuIdePccard.DeviceDesc% = 
          atapi_fujitsu_Inst, PCMCIA\FUJITSU-IDE-PC_CARD-DDF2
%*PNP0600.DeviceDesc% = atapi_Inst, *PNP0600 ; generic ESDI HDCs
%PCI\CC_0101.DeviceDesc% = pciide_Inst,,PCI\CC_0101

; ... other manufacturers' Models sections omitted

[atapi_Inst]
CopyFiles = @atapi.sys
LogConfig = esdilc1, esdilc2, esdilc3, esdilc4

; ... [atapi_Inst.Services] + service/EventLog-install omitted here

[esdilc1]
ConfigPriority=HARDWIRED
IOConfig=1f0-1f7(3ff::)
IoConfig=3f6-3f6(3ff::)
IRQConfig=14

[esdilc2]
ConfigPriority=HARDWIRED
IOConfig=170-177(3ff::)
IoConfig=376-376(3ff::)
IRQConfig=15

[esdilc3]
ConfigPriority=HARDWIRED
IOConfig=1e8-1ef(3ff::)
IoConfig=3ee-3ee(3ff::)
IRQConfig=11

[esdilc4]
; ...

[atapi_fujitsu_Inst.LogConfigOverride]
LogConfig = fujitsu.LogConfig0

[fujitsu.LogConfig0]
ConfigPriority=NORMAL
IOConfig=10@100-400%fff0
IRQConfig=14,15,5,7,9,11,12,3
PcCardConfig=1:0:0(W)
```

有关如何的一些示例**MfCardConfig**使用的条目，请参阅[支持 PC 卡，具有不完整配置注册地址](https://msdn.microsoft.com/library/windows/hardware/ff542774)。

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.FactDef**](inf-ddinstall-factdef-section.md)

 

 






