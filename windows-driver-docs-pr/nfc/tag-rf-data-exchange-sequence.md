---
title: 标记 RF 数据交换序列
description: 下图演示的状态序列 StateRfDiscovered 和 StateRfDataXchg 了各种读取器 / 编写器协议，如 T1T、 T2T、 T3T 和 ISO dep。
ms.assetid: F5911609-4531-44B3-9629-CD0A27D40324
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 810a3b407d4dbd914bbce43f4a730d08e1bee880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576862"
---
# <a name="tag-rf-data-exchange-sequence"></a>标记 RF 数据交换序列


下图演示的状态序列 StateRfDiscovered 和 StateRfDataXchg 了各种读取器 / 编写器协议，如 T1T、 T2T、 T3T 和 ISO dep。 过渡到 StateRfDiscovered RF 接口激活后发生。 在出现多个远程终结点或多个协议中 StateRfDiscovery，NFC CX 选择单个终结点和协议。 Bail 选项不支持由控制器的情况下，将在改进互操作性 NFC CX 中实现的 NFC DEP 通过 ISO DEP 首选项。 StateRfDiscovered 是其中 NFC CX 初始状态显示之前执行检查过渡到 StateRfDataXchg 过渡状态。 对于读取器/编写器模式，StateRfDataXchg 可划分为以下一系列 NDEF 操作： 检查 NDEF、 读取或写入 NDEF 后, 跟状态检查。 驱动程序还执行其他操作，例如格式设置，具体取决于从应用程序层请求此状态中的只读的、 低级别标记操作。 请注意，NFC CX 支持帧 RF 接口的所有 NCI 标准协议 （如 ISO15693） 除了 ISO dep。 ISO DEP RF 接口必须支持 NFC 控制器，用于支持 ISO DEP 协议。

![t1t rf 数据交换序列](images/rfdataexchangesequence.png)

以下说明了 T2T RF 数据交换序列：

![t2t rf 数据交换序列](images/t2trfdataexchangesequence.png)

以下说明了 T3T RF 数据交换序列：

![t3t rf 数据交换序列](images/t3trfdataexchangesequence.png)

以下说明了 ISO DEP RF 数据交换序列：

![iso dep rf 数据交换序列](images/iso-dep-rfdataexchangesequence.png)

没有要与远程 RF 终结点交换数据时，NFC CX StateRfDataXchg 在执行状态检查。 这用于确定是否远程 RF 终结点已超出范围从 DH。 序列图中所述，存在各种标记类型的检查可使用以下命令：

-   对于 NFC 论坛类型 1 标记，NFC CX 使用读取标识 (RID) 命令，这将返回 UID，来执行状态检查检测。

-   对于 NFC 论坛类型 2 标记，NFC CX 使用读取块命令，这将返回 16 位块数据，来执行状态检查检测。

-   NFC 论坛类型 3 标记，NFC CX 使用 RF\_T3T\_轮询\_CMD NCI 命令 (SENSF) 来执行状态检查检测。

-   对于 NFC 论坛类型 4 标记，NFC CX 使用空我块交换来执行状态检查检测。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  
