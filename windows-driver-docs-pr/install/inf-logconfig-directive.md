---
title: INF LogConfig 指令
description: LogConfig 指令将引用一个或多个由 INF 编写器定义的部分，每个部分都指定硬件资源的逻辑配置。
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
ms.openlocfilehash: 79b2662646c82765975fa144de2a80c33e80360e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818425"
---
# <a name="inf-logconfig-directive"></a>INF LogConfig 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**LogConfig** 指令将引用一个或多个由 INF 编写器定义的部分，其中每个部分都指定了硬件资源的逻辑配置−中断请求线路、内存范围、i/o 端口和可供设备使用的 DMA 通道。 每个 *日志配置节* 指定一组可由设备使用的其他总线相关硬件资源。

```inf
[DDInstall] | 
[DDInstall.LogConfigOverride] 
  
LogConfig=log-config-section[,log-config-section]...
```

非 PnP 设备的 INF 文件使用此指令创建基本配置。

PnP 设备的 INF 文件仅使用此指令创建替代配置。

**LogConfig** 指令引用的每个命名部分都具有以下形式：

```inf
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

## <a name="entries"></a>项


<a href="" id="configpriority-priority-value"></a>**ConfigPriority =**<em>priority-值</em>  
为此逻辑配置指定优先级值，如下所示：

<a href="" id="desired"></a>目标  
软配置，最佳。

<a href="" id="normal"></a>一般  
软配置，比所需的优化更少。 这是典型的设置。

如果在 DDInstall * 中定义了 *日志配置节*，则应指定 NORMAL [ * **。LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)部分，并且不能指定任何 *配置类型* 值。

<a href="" id="suboptimal"></a>最佳  
软配置，不如平时更好。

<a href="" id="hardreconfig"></a>HARDRECONFIG  
需要更改跳线更改。

<a href="" id="hardwired"></a>硬编码  
不能更改。

<a href="" id="restart"></a>重新启动  
需要重新启动才能生效。

<a href="" id="reboot"></a>要求  
这与重新启动相同。

<a href="" id="poweroff"></a>关机  
需要重启才能生效。

<a href="" id="disabled"></a>DISABLED  
硬件/设备处于禁用状态。

<a href="" id="dmaconfig--dmaattrs--dmanum--dmanum-----"></a>**DMAConfig =** \[*DMAattrs：* \]*DMANum* \[<strong>,</strong>DMANum \] .。。\]  
如果设备连接在仅具有8位 DMA 通道的总线上，并且设备使用标准系统 DMA，则 *DMAattrs* 是可选的。 否则，它可以是下列字母之一：

| Letter | 含义    |
|--------|------------|
| **D**  | 32位 DMA |
| **W**  | 16位 DMA |
| N  | 8位 DMA  |

 

如果 **设备使用的** 是 BUS 主机 DMA，则必须使用以下 (互斥的) 字母之一，指示所使用的 DMA 通道类型： **A**、 **B** 或 **F**。如果两者 **都未指定，** 则 **F** 假定为标准 DMA 通道。 **B**

*DMANum* 指定一个或多个以十进制数字表示的总线相关 DMA 通道，每个通道与下一个由逗号分隔 (，) 。

<a href="" id="ioconfig-io-range--io-range----"></a>**IOConfig =**<em>io 范围</em> \[ **io**<em>范围</em> \] .。。  
采用以下任一形式指定设备的一个或多个 i/o 端口范围：

<a href="" id="start-end---decode-mask---alias-offset---attr------type-1-i-o-range-"></a>*开始-结束* \[**(** \[*解码掩码* \] \[*：别名偏移* \] \[*： attr* \]**)** \] (类型 1 i/o 范围)   

<a href="" id="start"></a>*start*  
指定 i/o 端口范围的起始地址作为64位十六进制地址。

<a href="" id="end"></a>*端面*  
指定 i/o 端口范围的结束地址，也可以指定为64位的十六进制地址。

<a href="" id="decode-mask"></a>*解码掩码*  
定义别名类型，可以是以下任意类型：

| 掩码值 | 含义         | IOR_Alias 值 |
|------------|-----------------|------------------|
| **3ff**    | 10位解码   | 0x04             |
| **fff**    | 12位解码   | 0x10             |
| **ffff**   | 16位解码   | 0x00             |
| **0**      | 正解码 | 0xFF             |

 

<a href="" id="alias-offset-"></a>*别名偏移*   
未使用。

<a href="" id="attr"></a>*attr*  
指定给定范围在系统内存中时的字母 **M** 。 如果省略，则给定范围为 i/o 端口空间。

<a href="" id="size-min-max--align-mask----decode-mask---alias-offset---attr------type-2-i-o-range-"></a><em>大小</em> **@**<em>最小值-最大值</em> \[ **%**<em>对齐掩码</em> \] \[**(** \[*解码掩码* \] \[**：**<em>alias offset</em> \] \[ **：**<em>attr</em> \]) \] (类型 2 i/o 范围)   

<a href="" id="size"></a>*规格*  
指定将 i/o 端口范围作为32位十六进制值所需的字节数。

<a href="" id="min"></a>*min*  
指定最小可能的 i/o 端口范围的起始地址作为64位十六进制地址。

<a href="" id="max"></a>*数量*  
将 i/o 端口范围的最高可能结束地址指定为64位的十六进制地址。

<a href="" id="align-mask"></a>*对齐掩码*  
根据需要，还可以指定在按位与运算中使用的64位掩码，将 i/o 端口范围的开始与整数 (通常为32位或64位) 地址边界对齐。

<a href="" id="decode-mask"></a>*解码掩码*  
定义别名类型，可以是以下任意类型：

| 掩码值 | 含义         | IOR_Alias 值 |
|------------|-----------------|------------------|
| **3ff**    | 10位解码   | 0x04             |
| **fff**    | 12位解码   | 0x10             |
| **ffff**   | 16位解码   | 0x00             |
| **0**      | 正解码 | 0xFF             |

 

<a href="" id="alias-offset-"></a>*别名偏移*   
未使用。

<a href="" id="attr"></a>*attr*  
指定给定范围在系统内存中时的字母 **M** 。 如果省略，则给定范围为 i/o 端口空间。

<a href="" id="memconfig-mem-range--mem-range----"></a>**MemConfig =**<em>内存范围</em> \[ **，**<em>内存范围</em> \] .。。  
采用以下形式之一指定设备的一个或多个内存范围：

```inf
start-end[(attr)] | size@min-max[%align-mask][(attr)]
```

<a href="" id="start"></a>*start*  
指定作为64位十六进制值的设备内存范围的起始 (总线) 物理地址。

<a href="" id="end"></a>*端面*  
指定内存范围的结束物理地址，还指定为64位的十六进制值。

<a href="" id="attr"></a>*attr*  
将内存范围的特性指定为以下一个或多个字母：

| Letter | 含义                                             |
|--------|-----------------------------------------------------|
| **R**  | 只读                                           |
| **W**  | 只写                                          |
| **CD-RW** | 读取/写入                                          |
| **C**  | 允许合并写入                              |
| **H**  | 可缓存                                           |
| **F**  | Prefetchable                                        |
| **D**  | 卡解码寻址为32位，而不是24位 |

 

如果同时指定 **R** 和 **W** ，或者两者都未指定，则假定为读/写。

<a href="" id="size-"></a>*规格*   
指定内存范围中作为32位十六进制值所需的字节数。

<a href="" id="min--"></a>*min*   
指定最小可能的设备内存范围起始地址作为64位十六进制值。

<a href="" id="max"></a>*数量*  
将内存范围的最高可能结束地址指定为64位的十六进制值。

<a href="" id="align-mask-"></a>*对齐掩码*   
根据需要，还可以指定在 "位与" 运算中使用的64位掩码，以将设备内存范围的开始与整数 (通常为64位) 地址边界对齐。

如果省略对齐掩码，则默认内存对齐方式为4K 边界 (FFFFF000) 。

<a href="" id="irqconfig--irqattrs--irqnum--irqnum----"></a>**IRQConfig =** \[*IRQattrs：* \]*IRQNum* \[**，**<em>IRQNum</em> \] .。。  
如果设备使用与总线相关的、边缘触发的 IRQ，则省略 *IRQattrs* 。 否则，指定 **L** 以指示级别触发的 irq，如果设备可以共享此条目中列出的 irq 线路，则指定 **LS** 。

*IRQNum* 指定一个或多个与总线相对的 irq，设备可将其用作十进制数字，每个 irq 彼此之间用逗号分隔 (，) 。

<a href="" id="pccardconfig-configindex---memorycardbase1---memorycardbase2----attrs--"></a>**PcCardConfig =**<em>ConfigIndex</em> \[ **：** \[ *MemoryCardBase1* \] \[ **：**<em>MemoryCardBase2</em> \] \] \[ **(** <em>attrs</em> **)**\]  
配置 CardBus 注册和/或创建最多两个映射到设备属性空间的永久内存窗口。 驱动程序可以使用内存窗口从 ISR 访问属性空间。 指定以十六进制格式表示的所有数字值。

**PcCardConfig** 项的元素如下所示：

<a href="" id="configindex"></a>*ConfigIndex*  
指定 PCMCIA 总线上设备的8位 PCMCIA 配置索引。

<a href="" id="memorycardbase1"></a>*MemoryCardBase1*  
（可选）为第一个内存窗口指定32位基址。

<a href="" id="memorycardbase2"></a>*MemoryCardBase2*  
（可选）为第二个内存窗口指定32位基址。

<a href="" id="attrs"></a>*attrs*  
（可选）指定设备的一个或多个属性，用空格分隔。 无效的特性说明符会使整个 **PcCardConfig** 项无效。 如果提供了一个特定属性的多个说明符，则这些属性将应用于设备的单个 i/o 或内存窗口。 如果只提供了一个说明符，则该特性将应用于所有 windows (参见下面的示例) 。

具体而言，如果提供了多个说明符，则从左向右读取的第一个说明符将应用于第一个窗口，并将下一个说明符应用于第二个窗口。 单个 **PcCardConfig** 条目最多可以控制两个 i/o 窗口和两个内存窗口。 如果设备具有两个以上的内存窗口，则必须包含第二个 **PcCardConfig** 条目。

属性包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>W</strong></td>
<td align="left"><p>16位 i/o 数据路径。</p>
<p>如果 INF 指定了 <strong>LogConfig</strong> 指令，则默认值为8位。 如果未指定 <strong>LogConfig</strong> 指令，则驱动程序将使用16位 i/o。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S</strong><em>n</em></td>
<td align="left"><p>~ IOCS16 源。</p>
<p>如果 <em>n</em> 为0，则 ~ IOCS16 基于 datasize 位的值。 如果 n 为1，则 ~ IOCS16 基于设备的 ~ IOIS16 信号。 默认值为 <strong>S</strong>1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Z</strong><em>n</em></td>
<td align="left"><p>I/o 8 位，零等待状态。</p>
<p>如果 <em>n</em> 为1，则会出现8位 i/o 访问，但会出现零个附加等待状态。 如果 <em>n</em> 为0，则使用其他等待状态进行访问。 对于16位 i/o，此标志没有意义。 默认值为 <strong>Z</strong>0.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Xl</strong><em>n</em></td>
<td align="left"><p>I/o 等待状态。</p>
<p>如果 n 为1，则将发生16位系统访问，并且有一个额外的等待状态。 默认值为 <strong>Xl</strong>1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>M</strong></td>
<td align="left">16位内存数据路径。 默认值为8位。</td>
</tr>
<tr class="even">
<td align="left"><strong>M8</strong></td>
<td align="left">8位内存数据路径。</td>
</tr>
<tr class="odd">
<td align="left"><strong>XM</strong><em>n</em></td>
<td align="left"><p>内存等待状态，其中 n 可以是0、1、2或3。</p>
<p>此值确定对内存窗口进行16位访问的其他等待状态的数目。 默认值为 <strong>XM</strong>3.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>A</strong></td>
<td align="left">要映射为属性内存的内存范围。</td>
</tr>
<tr class="odd">
<td align="left"><strong>C</strong></td>
<td align="left">要映射为公用内存的内存范围 (默认) 。</td>
</tr>
</tbody>
</table>

 

例如，attrs 值为 (WB CA M XM1 XI0) 转换为以下内容：

第一个 i/o 窗口为16位

第二个 i/o 窗口8位

第一个内存窗口常见

第二个内存窗口是属性

内存为16位

内存窗口上有一个等待状态

I/o 窗口上的零等待状态

<a href="" id="mfcardconfig-configregbase-configoptions--ioresourceindex---attrs-----"></a>**MfCardConfig =**<em>ConfigRegBase</em>**：**<em>ConfigOptions</em> \[ **：**<em>IoResourceIndex</em> \] \[ **(** <em>attrs</em> **)** \] .。。指定多功能设备的一个功能的配置寄存器集的属性内存位置，如下所示：

<a href="" id="configregbase"></a>*ConfigRegBase*  
指定此多功能设备的此功能的配置寄存器属性偏移量。

<a href="" id="configoptions-"></a>*ConfigOptions*   
指定8位 PCMCIA 配置选项 "注册"。

<a href="" id="ioresourceindex-"></a>*IoResourceIndex*   
指定总线驱动程序的 **IOConfig** 条目的索引，该索引用于在配置 i/o 基和限制寄存器编程时使用。 此索引从零开始，即零指定此 *日志-config 节* 中的初始 **IOConfig** 条目。

<a href="" id="attrs-"></a>*attrs*   
如果设置为字母 **A**，则指示 PCMCIA 总线驱动程序在配置和状态寄存器中启用音频启用。

每个 **MfCardConfig** 条目都提供有关多功能设备的单个功能的信息。 如果一组 **LogConfig** 指令每个都引用 INF 的 DDInstall * 中的离散 *日志配置节*， [ * **LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)节中，每个 *日志配置节* 必须包含以相同顺序列出的 **MfCardConfig** 条目。

<a name="remarks"></a>备注
-------

可以在任何每个制造商、每个型号的 [**Inf *DDInstall* 部分**](inf-ddinstall-section.md)或 Inf DDInstall 下指定 **LogConfig** 指令 [***DDInstall*。LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)。

对于支持多种备用逻辑配置的非 PnP 设备，通常会在 *DDInstall* 节下定义一组 *日志-config 节*。 每个 *日志配置节* 指定一组离散的逻辑配置资源。 它还包括一个 **ConfigPriority** 条目，该条目根据每个逻辑配置对设备和驱动程序性能的影响、简化初始化等对每个逻辑配置进行排名。

对于 PnP 设备，PnP 管理器会为每个 PnP 设备分配一组逻辑硬件资源。 也就是说，PnP 管理器查询系统总线驱动程序，接收正在使用的每个设备 i/o 总线配置资源的报告，并分配每个设备的逻辑硬件资源集，以在使用所有此类资源时获得最佳系统范围平衡。

因此，对于 PnP 设备，将忽略 *DDInstall* 部分下的 **LogConfig** 指令。 若要替代用于 PnP 设备的总线报告的资源，请在 DDInstall 下包含 **LogConfig** 指令 [**_DDInstall_。LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)部分。 在这种情况下，将使用 *日志-config-部分* 中指定的资源，而不是总线报告的资源。

可以将平台扩展添加到 *DDInstall* 节，其中包含 **LogConfig** 指令或 [**_DDInstall_。LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)节，用于指定特定于平台或特定于 OS 的逻辑配置。 有关详细信息，请参阅 [创建 INF 文件](overview-of-inf-files.md)。

给定的 *日志配置节* 名称对于 inf 文件必须是唯一的，但它可以在相同设备的其他 INF *DDInstall* 部分中的 **LogConfig** 指令中引用。 在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

每个 *日志配置节* 中只能使用一个 **ConfigPriority** 条目。 每个其他条目中可以有多个条目，具体取决于设备的硬件资源需求。

一个或多个 **MfCardConfig =** 条目只能出现在 <em>DDInstall</em>的 **LogConfig** 指令所引用的 *日志配置节* 中 **。** 多功能设备 INF 的 LogConfigOverride 部分。 有关多功能设备的 INF 文件的详细信息，请参阅 [支持多功能设备](../multifunction/index.md)。

### <a name="logconfig-referenced-section-entries-and-values"></a>LogConfig-Referenced 节项和值

在 *日志配置部分* 中，系统安装程序将生成二进制逻辑配置记录并将其存储在注册表中。

INF 文件可以包含任意数量的每个设备的 *日志配置节*。 但是，每个此类部分必须包含用于安装一个设备的完整信息。 通常，INF 应以相同顺序指定其每个 *日志配置节* 中的条目。 INF 应按最适合于驱动程序如何初始化其设备的顺序指定每组条目。

如果给定设备有多个 *日志配置节* ，则在安装过程中仅使用其中一个 INF 部分。 此类 INF 文件部分控制将此类节与它在每个 **ConfigPriority** 中提供的值一起 *使用。* 也就是说，系统安装程序会尝试服从 INF 文件中的任何配置优先级，但如果找到与已安装的设备的冲突，则可能会选择较低的逻辑配置。

在安装过程中，将从给定的 *日志配置部分* 中的每个条目中只选择一个资源，并将其分配给特定设备。 如果特定设备需要多个相同类型的资源，则必须在其 *日志配置节* 中使用该类型的一组条目。

例如，若要确保特定设备的两个 i/o 端口范围，必须在该设备的 *日志-config-节* 中指定两个 **IOConfig =** 条目。 另一方面，如果设备不需要 IRQ，则其 INF 可以省略 *日志-config 节* 中的 **IRQConfig** 条目。

<a name="examples"></a>示例
--------

此示例显示了 PCMCIA 设备的一些有效 **PcCardConfig** 条目。

```inf
PcCardConfig=0:E0000:F0000(W)
PcCardConfig=0:E0000(M)
PcCardConfig=0::(W)
PcCardConfig=0(W)
```

此示例显示 **IOConfig** 条目中的类型 1 i/o 范围规范。 它指定一个 i/o 端口区域，大小为8个字节，可以从1F8、2F8 或3F8 开始。

```inf
IOConfig=1F8-1FF, 2F8-2FF, 3F8-3FF
```

与此相反，此示例在 **IOConfig** 项中显示一个类型 2 i/o 范围规范。 它指定一个 i/o 端口区域，大小为8个字节，可从300、308、310、318、320或328开始。

```inf
IOConfig=8@300-32F%FF8
```

此示例显示了一组用于四端口设备的 **IOConfig** 条目，每个条目指定一个 i/o 端口范围，该范围由下一次0x400 字节偏移。

```inf
IoConfig=0x200-0x21f
IoConfig=0x600-0x61f
IoConfig=0xA00-0xA1f
IoConfig=0xE00-0xE1f
```

下面两个示例显示了典型的 **MemConfig** 条目。

此示例指定可从 C0000 或 D0000 开始的32K 字节的内存区域。

```inf
MemConfig=C0000-C7FFF, D0000-D7FFF
```

此示例指定从64K 边界开始的32k 字节的内存区域。

```inf
MemConfig=8000@C0000-D7FFF%F0000
```

此示例演示系统 HDC 类 INF 文件如何为通用 ESDI 硬盘控制器设置几个 *日志配置节*，并使用 [ * **DDInstall *。**](inf-ddinstall-logconfigoverride-section.md)特定 IDE 控制器的 LogConfigOverride 部分。

```inf
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

有关如何使用 **MfCardConfig** 条目的一些示例，请参阅 [支持不完整的配置注册地址的 PC 卡](../multifunction/supporting-pc-cards-that-have-incomplete-configuration-register-addres.md)。

## <a name="see-also"></a>请参阅


[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。FactDef**](inf-ddinstall-factdef-section.md)

 

