---
title: RF 发现序列
description: 下图说明了 NFC CX 用于启动发现的 NCI 操作的顺序。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1116a0d40173b263fc1e92e46fc4ce50b3ea6bd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812721"
---
# <a name="rf-discovery-sequence"></a>RF 发现序列


下图说明了 NFC CX 用于启动发现的 NCI 操作的顺序。 从 StateRfIdle 中输入的 StateRfDiscovery 将触发启动 RF 发现序列。 在此状态下执行的主要操作集是配置 RF 发现参数、侦听模式路由表的可选配置，以及通过 RF discovery NCI 命令启用发现。 NFC 客户端驱动程序可以使用 SequencePreRfDiscStart 来添加非标准 NCI 命令，以优化发现进程。

![描述 NFC CX 开始发现所执行的 NCI 操作的序列图](images/staterfdiscoverysequence.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
