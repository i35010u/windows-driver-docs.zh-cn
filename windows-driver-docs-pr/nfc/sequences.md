---
title: 序列
description: 本主题介绍 NFC CX 驱动程序序列。
ms.assetid: 92FDF18F-B42B-43F2-914A-CA7E986EE0DF
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 718e1187b601056b626d6be87020432a4c7525d3
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385019"
---
# <a name="sequences"></a>序列


本主题介绍 NFC CX 驱动程序序列。

| 序列                    | 说明                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SequencePreInit             | 由 CX 在空闲到 init 状态转换期间进行调用 (即，NFC CX) 之前开始初始化。 \_NFC CX 未向 nfc 控制器发送包括核心重置 CMD 的 NCI 命令 \_ 。 在此序列中，客户端可以调用任何非 NCI 命令。 不应将 NCI 命令发送到控制器，因为核心 \_ 重置 \_ CMD 或核心 \_ INIT cmd 都未 \_ 发送到控制器。 |
| SequenceInitComplete        | 由 CX 在完成 NFC CX 初始化之后立即调用，其中包括 NCI reset、NCI 初始化和配置 NFC 控制器。                                                                                                                                                                                                                                          |
| SequencePreRfDiscStart      | 在 RF 发现开始之前由 CX 调用，即通过 RF \_ 发现 \_ CMD。 客户端驱动程序可以利用此机会来执行任何相关 RF 配置，包括对发现循环的任何优化。                                                                                                                                                                                        |
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
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)