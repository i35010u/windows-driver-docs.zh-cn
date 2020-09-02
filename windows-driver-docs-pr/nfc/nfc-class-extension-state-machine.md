---
title: NFC 类扩展状态机
description: NFC CX 状态机的内部设计如下所示。
ms.assetid: A131F881-C05A-44FF-A7A6-FD40BA344BD0
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba24b1f61baf8c4db24dc15ea49e21e1f3eeef32
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382495"
---
# <a name="nfc-class-extension-state-machine"></a>NFC 类扩展状态机


NFC CX 状态机的内部设计如下所示。 NFC CX 指定的各种状态以及导致状态转换的内部和外部事件都在关系图中捕获。 请注意，某些状态之间的某些转换不会显示在关系图中以方便阅读。 下面更详细地介绍了如何将状态连同映射到 NCI RF 状态机。

![nfc cx 状态机](images/statemachine.png)

| 状态             | 说明                                                                                                                                                                                                                                                                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| StateIdle         | 当 NFC 设备处于开启状态，但没有 NCI 命令发送到控制器时，或在 NCI 操作期间发生了不可恢复的错误时，将进入 StateIdle。                                                                                                                                                                                         |
| StateInit         | 将硬件 \_ 操作启动发送到 NFC CX 时，会输入 StateInit。 NCI reset、NCI 初始化和 NFC 芯片组配置在此状态下发生。 此表中下面 (的所有后续状态) 在此状态完成后发生。                                                                                                          |
| StateRfIdle       | NFC 控制器已成功初始化，但 RF 轮询循环处于禁用状态 (也就是说，轮询和侦听阶段都处于禁用状态或未) 配置。 当无需 NFC 操作时，设备会进入 StateRfIdle。 当处于此状态时，将启用 UMDF 空闲检测计时器，并在此时间段后过期，芯片 deinitialized |
| StateRfDiscovery  | NFC 控制器将其发现循环配置为轮询和/或侦听阶段。 在启用发现循环之前，某些发现参数的配置也会处于此状态。                                                                                                                                                    |
| StateRfDiscovered | 发现并选择了 RF 远程终结点，并且已激活 RF 接口以便设备主机与其通信。 这是一种过渡性状态。                                                                                                                                                                                      |
| StateRfDataXchg   | 设备主机和 RF 远程终结点在轮询或侦听模式下主动交换数据。 此状态涵盖 \_ \_ \_ \_ NCI RF 状态机中活动的状态 RFST 轮询活动或 RFST 侦听。                                                                                                                                             |
| StateRecovery     | 当 NFC 设备将核心 \_ RSET \_ contoso.ntf 发送到主机时，或者如果出现严重 i/o 错误，将进入此状态，NCI 操作期间会发生超时。 NFC CX 尝试通过重置并重新初始化控制器来执行 NCI 恢复。 如果恢复成功，正常操作将恢复，否则状态机将转换为 StateIdle。  |
| StateShutdown     | NFC 设备即将关闭。 这是一种过渡性状态。 此状态完成后，状态机将转换为 StateIdle。                                                                                                                                                                                                       |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)