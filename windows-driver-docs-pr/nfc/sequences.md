---
title: 序列
description: 本主题介绍 NFC CX 驱动程序序列。
ms.assetid: 92FDF18F-B42B-43F2-914A-CA7E986EE0DF
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e2271b23018f157c61b68e2bfb9665c64981d3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826175"
---
# <a name="sequences"></a>序列


本主题介绍 NFC CX 驱动程序序列。

| 序列                    | 描述                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SequencePreInit             | 由 CX 在空闲到 init 状态转换期间（即，由 NFC CX 初始化之前）调用。 NFC CX 未向 NFC 控制器发送 NCI 命令，包括核心\_重置\_CMD。 在此序列中，客户端可以调用任何非 NCI 命令。 不应将 NCI 命令发送到控制器，因为\_CMD 或核心\_\_INIT 中的核心\_重置均未发送到控制器。 |
| SequenceInitComplete        | 由 CX 在完成 NFC CX 初始化之后立即调用，其中包括 NCI reset、NCI 初始化和配置 NFC 控制器。                                                                                                                                                                                                                                          |
| SequencePreRfDiscStart      | 由 CX 在 RF 发现开始之前调用，即通过 RF\_发现\_CMD。 客户端驱动程序可以利用此机会来执行任何相关 RF 配置，包括对发现循环的任何优化。                                                                                                                                                                                        |
| SequenceRfDiscStartComplete | 在开始 RF 发现后，由 CX 立即调用。 可以通过此扩展点支持任何配置后发现启动。                                                                                                                                                                                                                                                      |
| SequencePreRfDiscStop       | 由 CX 在停止 RF 发现循环之前调用。                                                                                                                                                                                                                                                                                                                                                    |
| SequenceRfDiscStopComplete  | 在发现循环停止之后立即调用。 客户端驱动程序可以使用此扩展点来启用任何备用模式配置。                                                                                                                                                                                                                                                         |
| SequencePreNfceeDisc        | 在 NFCEE 发现开始之前由 CX 调用。 NFCEE 发现在发现循环停用的情况下发生。 客户端驱动程序可以使用此序列来启用任何内部 NFC NFCEE 接口，这些接口可能已在电源优化后禁用了初始化后。                                                                                                                         |
| SequenceNfceeDiscComplete   | 立即调用 NFCEE 发现操作。                                                                                                                                                                                                                                                                                                                                                       |
| SequencePreShutdown         | 在关闭之前调用。                                                                                                                                                                                                                                                                                                                                                                       |
| SequenceShutdownComplete    | 在关闭序列完成后由 CX 调用。 客户端驱动程序可以清除维护的任何 NCI 状态。                                                                                                                                                                                                                                                                                               |
| SequencePreRecovery         | 如果因致命故障而需要执行恢复顺序，由 CX 调用。 客户端驱动程序可以使用此序列捕获 RAM 转储以用于诊断目的。                                                                                                                                                                                                                                    |
| SequenceRecoveryComplete    | 在完成恢复序列后以及当驱动程序恢复到工作状态之后由 CX 调用                                                                                                                                                                                                                                                                                             |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

