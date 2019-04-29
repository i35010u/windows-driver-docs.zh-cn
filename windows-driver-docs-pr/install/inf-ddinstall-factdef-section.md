---
title: INF DDInstall.FactDef 节
description: 最终用户可能安装的任何手动安装非 PnP 设备，应在 INF 中使用此部分。
ms.assetid: df2d46da-4e69-4e3c-b208-1ae0a0f771c9
keywords:
- INF DDInstall.FactDef 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.FactDef Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f599ee65e3f3cd977cdd8a8d474bdd8dd2a6be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378052"
---
# <a name="inf-ddinstallfactdef-section"></a>INF DDInstall.FactDef 节


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

最终用户可能安装的任何手动安装非 PnP 设备，应在 INF 中使用此部分。 本部分中指定工厂默认硬件配置设置，例如总线相对 I/O 端口和 IRQ （如果有），此类卡。

```ini
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

## <a name="entries"></a>条目


<a href="" id="configpriority-priority-value"></a>**ConfigPriority=**<em>Priority-Value</em>  
指定此工厂默认逻辑配置以下优先级值之一。

| 优先级值 | 含义                                                                                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FORCECONFIG    | 指定标识的即插即用的管理器必须向设备分配的资源的强制的配置。                                                                                            |
| 所需的        | 提供最高的设备性能。 PnP 管理器可以使用此配置来动态配置设备。                                                                                    |
| NORMAL         | 提供了更高的设备性能比 SUBOPTIMAL，但更低比所需的性能。 这是典型的优先级值。 PnP 管理器可以使用此配置来动态配置设备。 |
| 非最优     | 提供最低的设备性能。 此配置不合适，但将起作用。 PnP 管理器可以动态地配置此配置。                                              |
| 重新启动        | 需要重启系统。                                                                                                                                                                                |
| 重新启动         | 需要重启系统。                                                                                                                                                                                |
| 关闭       | 需要一个电源周期。                                                                                                                                                                                   |
| HARDRECONFIG   | 不需要跳线更改。                                                                                                                                                                                 |
| 硬编码      | 不能更改。                                                                                                                                                                                        |
| 已禁用       | 指示设备已被禁用。                                                                                                                                                                    |

 

<a href="" id="dmaconfig--dmaattrs--dmanum"></a>**DMAConfig =**\[<em>DMAattrs</em>**:**\]*DMANum*  
指定以十进制数的总线相对 DMA 通道。 *DMAattrs*是可选的如果具有唯一的 8 位 DMA 通道的总线上连接设备和设备使用标准系统 DMA。 否则，它可以是一个字母**D**的 32 位 DMA **W**的 16 位 DMA 并**N**的 8 位 DMA 与**M**如果设备使用主总线 DMA，且一个指示使用 DMA 通道的类型的以下 （互斥） 字母：**一个**， **B**，或**F**。如果没有**A**， **B**，或**F**是指定，则假定标准 DMA 通道。

<a href="" id="ioconfig-io-range"></a>**IOConfig=**<em>io-range</em>  
采用以下格式指定该设备的 I/O 端口范围：

```ini
start-end[([decode-mask][:alias-offset][:attr])]
```

<a href="" id="start"></a>*start*  
为 64 位十六进制值指定 I/O 端口范围 （总线相对） 起始地址。

<a href="" id="end-"></a>*end*   
也可用作 64 位十六进制值指定 I/O 端口范围的结束地址。

<a href="" id="decode-mask-"></a>*decode-mask*   
定义别名类型，并且可以为下列任一。

| 掩码值 | 含义         | IOR_Alias 值 |
|------------|-----------------|------------------|
| **3ff**    | 10 位解码   | 0x04             |
| **fff**    | 12 位解码   | 0x10             |
| **ffff**   | 16 位解码   | 0x00             |
| **0**      | 正解码 | 0xFF             |

 

<a href="" id="alias-offset"></a>*alias-offset*  
不使用。

<a href="" id="attr"></a>*attr*  
指定以字母**M**如果指定的范围是在系统内存中。 如果省略，则指定的范围处于 I/O 端口空间。

<a href="" id="memconfig-mem-range"></a>**MemConfig=**<em>mem-range</em>  
采用以下格式指定该设备的内存范围：

```ini
start-end[(attr)]
```

<a href="" id="start"></a>*start*  
为 64 位十六进制值指定设备的内存范围的起始 （总线相对） 的地址。

<a href="" id="end-"></a>*end*   
也可用作 64 位十六进制值指定内存范围的结束的地址。

<a href="" id="attr"></a>*attr*  
指定为一个或多个以下字母的内存范围的属性：

-   **R** （只读）
-   **W** （只写）
-   **RW** （读/写）
-   **C** （组合允许写入）
-   **H** （缓存）
-   **F** (prefetchable)
-   **D** (卡解码寻址为 32 位，而不是 24 位)

如果这两个**R**并**W**指定或如果属性均未指定，则假定为读/写。

<a href="" id="irqconfig--irqattrs--irqnum"></a>**IRQConfig=**\[<em>IRQattrs</em>**:**\]*IRQNum*  
指定以十进制数的设备使用总线相对 IRQ。 *IRQattrs*如果设备使用总线相对，边缘触发 IRQ 省略。 否则，指定**L**以指示级别触发的 IRQ，并**LS**如果设备可以共享此项中列出的 IRQ 线路。

<a name="remarks"></a>备注
-------

指定*DDInstall*部分必须在每个制造商下的特定于设备的项中引用*模型*INF 文件部分。 不区分大小写的扩展*安装的部分名称*所示在正式语法语句可插入到此类<em>DDInstall</em>**。FactDef**跨操作系统的系统和/或跨平台 INF 文件中的节名称。 有关这些系统定义的扩展的详细信息，请参阅[创建一个 INF 文件](overview-of-inf-files.md)。

本部分必须包含完整的出厂默认值安装一台设备的信息。 INF 应指定此组条目按最佳顺序适用于该驱动程序如何初始化其设备。 如有必要，它可以有多个任何特定类型的条目。

例如，使用两个 DMA 通道的设备 INF 将具有两个**DMAConfig =** 中的行及其<em>DDInstall</em>**。FactDef**部分。

此外应使用手动安装设备的出厂默认值逻辑的配置设置可以为其更改的 INF 文件**LogConfig**指令及其*DDInstall*部分。 一般情况下，此类 INF 应在每个指定的条目，其日志配置节，并在其<em>DDInstall</em>**。FactDef**部分中的顺序相同。

<a name="examples"></a>示例
--------

这**IOConfig**条目指定的 I/O 端口区域大小，可以从开始 2F8 的 8 个字节。

```ini
IOConfig=2F8-2FF
```

这**MemConfig**条目指定可以从开始 D0000 32 kb 的内存区域。

```ini
MemConfig=D0000-D7FFF
```

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






