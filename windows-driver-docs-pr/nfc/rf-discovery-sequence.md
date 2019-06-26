---
title: RF 发现序列
description: 下图说明了用于启动发现执行 NFC CX NCI 操作的顺序。
ms.assetid: 392F8A06-262D-4CF9-B510-C3FE86291026
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40a312190e7d84499c2ecc1940fdbfd5dcf07599
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386509"
---
# <a name="rf-discovery-sequence"></a>RF 发现序列


下图说明了用于启动发现执行 NFC CX NCI 操作的顺序。 输入从 StateRfIdle StateRfDiscovery 触发开始 RF 发现序列。 在此状态下执行的操作组主要是 RF 发现参数的配置、 可选配置为侦听模式路由表，以及启用通过 RF 发现发现 NCI 命令。 NFC 客户端驱动程序可以使用 SequencePreRfDiscStart 添加非标准 NCI 命令，以优化发现过程。

![序列图描绘了由 NFC CX 执行启动发现的 NCI 操作](images/staterfdiscoverysequence.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

