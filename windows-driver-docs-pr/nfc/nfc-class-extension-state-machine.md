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
ms.openlocfilehash: 3e9e0689395dac821ae0136d2e022c9a07d90cb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567245"
---
# <a name="nfc-class-extension-state-machine"></a>NFC 类扩展状态机


NFC CX 状态机的内部设计如下所示。 在关系图中捕获由 NFC CX 和会导致状态转换的内部和外部事件指定的各种状态。 请注意，某些状态之间的某些转换不显示在关系图中以便于阅读。 以及映射到 NCI RF 状态机的状态是下面做进一步说明。

![nfc cx 状态机](images/statemachine.png)

| 状态             | 描述                                                                                                                                                                                                                                                                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| StateIdle         | NFC 设备已启动但没有 NCI 命令发送到控制器，或 NCI 操作期间发生不可恢复的错误时输入 StateIdle。                                                                                                                                                                                         |
| StateInit         | 输入 StateInit 时硬件\_操作开始发送到 NFC CX。 重置 NCI，NCI 初始化并 NFC 芯片集配置将在此状态后发生。 所有后续状态 (如下此表中) 的此状态下完成操作后发生。                                                                                                          |
| StateRfIdle       | NFC 控制器初始化成功，但禁止将 RF 轮询循环 （即，同时轮询和侦听阶段被禁用或未配置）。 在设备进入 StateRfIdle 时没有 NFC 操作是必需的。 UMDF 空闲检测计时器处于启用状态时在此状态下和 post deinitialized 此计时器，芯片集的过期时间 |
| StateRfDiscovery  | NFC 控制器已配置为任一轮询其发现循环和/或侦听阶段。 某些发现参数的配置也恰好在此状态下启用发现循环之前。                                                                                                                                                    |
| StateRfDiscovered | RF 远程终结点被发现和选定并且已为要与之进行通信的设备主机激活 RF 接口。 这是一种转换状态。                                                                                                                                                                                      |
| StateRfDataXchg   | 设备主机和 RF 远程终结点正在积极地交换数据中任一轮询或侦听模式。 此状态介绍这两个状态 RFST\_轮询\_处于活动状态或 RFST\_侦听\_NCI RF 状态机中处于活动状态。                                                                                                                                             |
| StateRecovery     | NFC 设备具有发送一个核心时，将进入此状态\_RSET\_NTF 到主机或 NCI 操作过程中出现 I/O 错误，如果发生超时。 NFC CX 尝试执行 NCI 恢复的重置并重新初始化控制器。 正常操作恢复恢复是否成功，否则状态机转换到 StateIdle。  |
| StateShutdown     | NFC 设备即将关闭。 这是一种转换状态。 在此状态下完成，状态机转换为 StateIdle。                                                                                                                                                                                                       |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

