---
title: 标记 RF 数据交换序列
description: 下图说明了各种读取器-编写器协议（如 T1T、T2T、T3T 和 ISO-DEP）的 StateRfDiscovered 和 StateRfDataXchg 的状态顺序。
ms.assetid: F5911609-4531-44B3-9629-CD0A27D40324
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afc480e6142acd70cf6e14926869b38135c36ad5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827360"
---
# <a name="tag-rf-data-exchange-sequence"></a>标记 RF 数据交换序列


下图说明了 StateRfDiscovered 和 StateRfDataXchg 的状态序列，适用于各种读取器-编写器协议，如 T1T、T2T、T3T 和 ISO-DEP。 在 RF 接口激活之后发生到 StateRfDiscovered 的转换。 对于多个远程终结点或 StateRfDiscovery 中的多个协议，NFC CX 选择单个终结点和协议。 在 NFC CX 中实现的 NFC-dep 的首选项在 NFC CX 中实现，因为控制器不支持 case 定位选项。 StateRfDiscovered 是一个过渡状态，其中 NFC CX 在转换到 StateRfDataXchg 之前执行初始状态检查。 对于读取器/写入器模式，StateRfDataXchg 划分为以下 NDEF 操作序列：检查 NDEF、读取或写入 NDEF，然后执行状态检查。 驱动程序还会根据应用程序层的请求，在此状态下执行其他操作，例如格式设置、只读、低级别标记操作。 请注意，NFC CX 支持所有 NCI 标准协议（ISO15693）的帧射频接口（ISO-DEP 除外）。 ISO-DEP 控制器必须支持用于支持 ISO DEP 协议的 NFC 控制器。

![t1t rf 数据交换序列](images/rfdataexchangesequence.png)

下面说明了 T2T RF 数据交换序列：

![t2t rf 数据交换序列](images/t2trfdataexchangesequence.png)

下面说明了 T3T RF 数据交换序列：

![t3t rf 数据交换序列](images/t3trfdataexchangesequence.png)

下面说明了 ISO-DEP 射频数据交换序列：

![iso-dep rf 数据交换序列](images/iso-dep-rfdataexchangesequence.png)

当没有可与远程 RF 终结点交换的数据时，NFC CX 会在 StateRfDataXchg 中执行状态检查。 这用于确定远程 RF 终结点是否已从 DH 移出范围。 如序列图所述，以下命令用于各种标记类型的状态检查：

-   对于 NFC 论坛类型1标记，NFC CX 使用读取标识（RID）命令，该命令返回 UID 来执行状态检查检测。

-   对于 NFC 论坛类型2标记，NFC CX 使用 READ block 命令，该命令返回16字节块数据，以执行状态检查检测。

-   对于 NFC 论坛类型3标记，NFC CX 使用 RF\_T3T\_轮询\_CMD NCI 命令（SENSF）来执行状态检查检测。

-   对于 NFC 论坛类型4标记，NFC CX 使用空的 I 块交换来执行状态检查检测。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
