---
title: INF DDInstall.FactDef 节
description: 对于最终用户可能会安装的任何手动安装的非 PnP 设备，本部分应该用于 INF。
keywords:
- INF DDInstall. FactDef 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.FactDef Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 264af663f4096911ad8c939b0574f9809c1f0a69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790565"
---
# <a name="inf-ddinstallfactdef-section"></a>INF DDInstall.FactDef 节


**注意**  如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

对于最终用户可能会安装的任何手动安装的非 PnP 设备，本部分应该用于 INF。 此部分指定出厂默认硬件配置设置，如总线相关 i/o 端口和 IRQ (此类卡的任何) 。

```inf
[install-section-name.FactDef] |
[install-section-name.nt.FactDef] | 
[install-section-name.ntx86.FactDef] | 
[install-section-name.ntarm.FactDef] |  (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.FactDef] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.FactDef] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.FactDef]  (Windows XP and later versions of Windows)
 
ConfigPriority=Priority-Value
[DMAConfig=[DMAattrs:]DMANum]
[IOConfig=io-range]
[MemConfig=mem-range]
[IRQConfig=[IRQattrs:]IRQNum]
... 
```

## <a name="entries"></a>项


<a href="" id="configpriority-priority-value"></a>**ConfigPriority =**<em>Priority-值</em>  
为此工厂默认逻辑配置指定以下优先级值之一。

| 优先级值 | 含义                                                                                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FORCECONFIG    | 指定强制配置，该配置标识 PnP 管理器必须分配给设备的资源。                                                                                            |
| 目标        | 提供最高的设备性能。 PnP 管理器可以通过此配置动态配置设备。                                                                                    |
| NORMAL         | 提供的设备性能高于不理想，但性能低于所需的性能。 这是典型的优先级值。 PnP 管理器可以通过此配置动态配置设备。 |
| 最佳     | 提供最低的设备性能。 此配置不是必需的，但它将起作用。 PnP 管理器可以动态配置此配置。                                              |
| RESTART        | 需要重新启动系统。                                                                                                                                                                                |
| 要求         | 需要重新启动系统。                                                                                                                                                                                |
| 关机       | 需要电源周期。                                                                                                                                                                                   |
| HARDRECONFIG   | 需要跳线更改。                                                                                                                                                                                 |
| 硬编码      | 不能更改。                                                                                                                                                                                        |
| DISABLED       | 指示设备已禁用。                                                                                                                                                                    |

 

<a href="" id="dmaconfig--dmaattrs--dmanum"></a>**DMAConfig =** \[<em>DMAattrs</em>**：** \] *DMANum*  
将总线相关 DMA 通道指定为十进制数字。 如果设备连接在仅具有8位 DMA 通道的总线上，并且设备使用标准系统 DMA，则 *DMAattrs* 是可选的。 否则，它可以是用于32位 DMA 的字母 **D** 、16位 Dma 的 **W** 和8位 dma 的 **N** ; 如果设备使用的是总线主控 dma，则使用 M，使用 **M** ，使用以下 (互斥的) 字母之一，这些字母表示使用的 DMA 通道的类型： **A**、 **B** 或 **F**。如果未指定 **a**、 **B** 或 **F** ，则假定为标准 DMA 通道。

<a href="" id="ioconfig-io-range"></a>**IOConfig =**<em>io 范围</em>  
按以下格式指定设备的 i/o 端口范围：

```inf
start-end[([decode-mask][:alias-offset][:attr])]
```

<a href="" id="start"></a>*start*  
指定以64位十六进制值形式表示的 i/o 端口范围 (与总线相关的) 起始地址。

<a href="" id="end-"></a>*终点*   
指定 i/o 端口范围的结束地址，也可以指定为64位的十六进制值。

<a href="" id="decode-mask-"></a>*解码掩码*   
定义别名类型，可以是以下任意类型。

| 掩码值 | 含义         | IOR_Alias 值 |
|------------|-----------------|------------------|
| **3ff**    | 10位解码   | 0x04             |
| **fff**    | 12位解码   | 0x10             |
| **ffff**   | 16位解码   | 0x00             |
| **0**      | 正解码 | 0xFF             |

 

<a href="" id="alias-offset"></a>*别名偏移*  
未使用。

<a href="" id="attr"></a>*attr*  
指定指定范围在系统内存中时的字母 **M** 。 如果省略，则指定的范围为 i/o 端口空间。

<a href="" id="memconfig-mem-range"></a>**MemConfig =**<em>mem 范围</em>  
按以下格式指定设备的内存范围：

```inf
start-end[(attr)]
```

<a href="" id="start"></a>*start*  
指定作为64位十六进制值的设备内存范围的起始 (总线) 地址。

<a href="" id="end-"></a>*终点*   
指定内存范围的结束地址，还指定为64位的十六进制值。

<a href="" id="attr"></a>*attr*  
将内存范围的特性指定为以下一个或多个字母：

-   **R** (只读) 
-   **W** (只写) 
-   读/写 (**RW**) 
-   **C** (允许的组合写入) 
-   **H** (可缓存) 
-   **F** (prefetchable) 
-   **D** (卡解码寻址为32位，而不是24位) 

如果同时指定 **R** 和 **W** ，或者两者都未指定，则假定为读/写。

<a href="" id="irqconfig--irqattrs--irqnum"></a>**IRQConfig =** \[<em>IRQattrs</em>**：** \] *IRQNum*  
指定设备使用的总线相对 IRQ，作为一个十进制数。 如果设备使用与总线相关的、边缘触发的 IRQ，则省略 *IRQattrs* 。 否则，请指定 **L** 以指示级别触发的 IRQ，如果设备可以共享此条目中列出的 irq 线路，则指定 **LS** 。

<a name="remarks"></a>备注
-------

在 INF 文件的 "每制造商的 *型号*" 部分下，必须在特定于设备的条目中引用指定的 *DDInstall* 部分。 在正式语法语句中显示的 *安装节名称* 不区分大小写的扩展可以插入到此类 <em>DDInstall</em>中 **。** 跨操作系统和/或跨平台 INF 文件中的 FactDef 节名称。 有关这些系统定义的扩展的详细信息，请参阅 [创建 INF 文件](overview-of-inf-files.md)。

此部分必须包含完整的出厂默认信息，以便安装一个设备。 INF 应按最适合于驱动程序如何初始化其设备的顺序指定这组条目。 如有必要，它可以有多个特定类型的条目。

例如，使用两个 DMA 通道的设备的 INF 在其 <em>DDInstall</em>中将有两个 **DMAConfig =** 行 **。FactDef** 部分。

可以更改其出厂默认逻辑配置设置的手动安装设备的 INF 文件还应在其 *DDInstall* 节中使用 **LogConfig** 指令。 通常，此类 INF 应该指定其每个日志配置节及其 <em>DDInstall</em>中的条目 **。** 按相同顺序 FactDef 部分。

<a name="examples"></a>示例
--------

此 **IOConfig** 条目指定一个 i/o 端口区域，大小为8个字节，可以从2F8 开始。

```inf
IOConfig=2F8-2FF
```

此 **MemConfig** 条目指定可从 D0000 开始的32k 字节的内存区域。

```inf
MemConfig=D0000-D7FFF
```

## <a name="see-also"></a>请参阅


[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *LogConfig**](inf-logconfig-directive.md)

 

 






