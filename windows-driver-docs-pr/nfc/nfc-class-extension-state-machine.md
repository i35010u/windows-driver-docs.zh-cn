---
title: NFC 类扩展状态机
description: NFC CX 状态机的内部设计如下所示。
ms.assetid: A131F881-C05A-44FF-A7A6-FD40BA344BD0
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3cda10e06792f9b56782cf3c01856c128d80a44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831884"
---
# <a name="nfc-class-extension-state-machine"></a>NFC 类扩展状态机


NFC CX 状态机的内部设计如下所示。 NFC CX 指定的各种状态以及导致状态转换的内部和外部事件都在关系图中捕获。 请注意，某些状态之间的某些转换不会显示在关系图中以方便阅读。 下面更详细地介绍了如何将状态连同映射到 NCI RF 状态机。

![nfc cx 状态机](images/statemachine.png)

| 省/市/自治区             | 描述                                                                                                                                                                                                                                                                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| StateIdle         | 当 NFC 设备处于开启状态，但没有 NCI 命令发送到控制器时，或在 NCI 操作期间发生了不可恢复的错误时，将进入 StateIdle。                                                                                                                                                                                         |
| StateInit         | 当硬件\_操作开始发送到 NFC CX 时，将输入 StateInit。 NCI reset、NCI 初始化和 NFC 芯片组配置在此状态下发生。 完成此状态之后，所有后续状态（在此表中）都将发生。                                                                                                          |
| StateRfIdle       | NFC 控制器已成功初始化，但 RF 轮询循环处于禁用状态（也就是说，已禁用或未配置轮询和侦听阶段）。 当无需 NFC 操作时，设备会进入 StateRfIdle。 当处于此状态时，将启用 UMDF 空闲检测计时器，并在此时间段后过期，芯片 deinitialized |
| StateRfDiscovery  | NFC 控制器将其发现循环配置为轮询和/或侦听阶段。 在启用发现循环之前，某些发现参数的配置也会处于此状态。                                                                                                                                                    |
| StateRfDiscovered | 发现并选择了 RF 远程终结点，并且已激活 RF 接口以便设备主机与其通信。 这是一个过渡状态。                                                                                                                                                                                      |
| StateRfDataXchg   | 设备主机和 RF 远程终结点在轮询或侦听模式下主动交换数据。 此状态涵盖 NCI RF 状态机中处于活动状态的\_轮询\_活动或 RFST\_侦听\_。                                                                                                                                             |
| StateRecovery     | 当 NFC 设备将核心\_RSET\_CONTOSO.NTF 发送到主机时，或者如果出现严重 i/o 错误，将进入此状态，NCI 操作期间会发生超时。 NFC CX 尝试通过重置并重新初始化控制器来执行 NCI 恢复。 如果恢复成功，正常操作将恢复，否则状态机将转换为 StateIdle。  |
| StateShutdown     | NFC 设备即将关闭。 这是一个过渡状态。 此状态完成后，状态机将转换为 StateIdle。                                                                                                                                                                                                       |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

