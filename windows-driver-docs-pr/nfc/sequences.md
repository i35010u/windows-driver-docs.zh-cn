---
title: 序列
description: 本主题介绍 NFC CX 驱动程序序列。
ms.assetid: 92FDF18F-B42B-43F2-914A-CA7E986EE0DF
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96b61a609ba0901c8ebb541dee833353aebc4238
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522411"
---
# <a name="sequences"></a>序列


本主题介绍 NFC CX 驱动程序序列。

| 序列                    | 描述                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SequencePreInit             | Init 状态转换到空闲期间调用 CX (即，在开始通过 NFC CX 初始化之前)。 包括 CORE 没有 NCI 命令\_重置\_CMD 已发送到 NFC 控制器通过 NFC CX。 在此序列中，客户端可以调用任何非 NCI 命令。 NCI 命令不应以来都不核心发送到控制器\_重置\_CMD 和核心\_INIT\_CMD 已发送到控制器。 |
| SequenceInitComplete        | 其中包括 NCI 重置、 NCI 初始化和配置的 NFC 控制器 NFC CX 的初始化完成后立即调用由 CX。                                                                                                                                                                                                                                          |
| SequencePreRfDiscStart      | 调用 CX 之前启动的 RF 发现，即通过 RF\_发现\_cmd。 客户端驱动程序可以使用此机会来执行任何相关的 RF 配置，包括对发现循环的任何优化。                                                                                                                                                                                        |
| SequenceRfDiscStartComplete | RF 发现启动后立即调用由 CX。 通过此扩展点，可以支持任何配置后发现启动。                                                                                                                                                                                                                                                      |
| SequencePreRfDiscStop       | 在停止 RF 发现循环之前调用由 CX。                                                                                                                                                                                                                                                                                                                                                    |
| SequenceRfDiscStopComplete  | 发现循环已停止后立即调用。 客户端驱动程序可以使用此扩展性点以启用备用服务器模式的任何配置。                                                                                                                                                                                                                                                         |
| SequencePreNfceeDisc        | 由启动的 NFCEE 发现 CX 之前调用。 NFCEE 发现发生停用的发现循环。 客户端驱动程序可以使用此序列来启用任何内部的 NFC NFCEE 接口，这可能是已禁用后的初始化为电源优化。                                                                                                                         |
| SequenceNfceeDiscComplete   | 立即调用 post NFCEE 发现操作。                                                                                                                                                                                                                                                                                                                                                       |
| SequencePreShutdown         | 在开始关闭之前调用。                                                                                                                                                                                                                                                                                                                                                                       |
| SequenceShutdownComplete    | 由 CX 关闭序列完成后调用。 客户端驱动程序可以清理维护任何 NCI 状态。                                                                                                                                                                                                                                                                                               |
| SequencePreRecovery         | 如果需要执行由于致命故障恢复顺序由 CX 调用。 客户端驱动程序可以使用此序列来捕获内存转储以进行诊断。                                                                                                                                                                                                                                    |
| SequenceRecoveryComplete    | 由 CX 后完成的恢复顺序以及驱动程序是恢复到工作状态时调用                                                                                                                                                                                                                                                                                             |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

