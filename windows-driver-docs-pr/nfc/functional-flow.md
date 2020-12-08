---
title: 智能卡的功能流
description: 智能卡发现后对 NDEF 消息进行分层读取和写入的流程图和简短说明。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76d997b410bfec7bedde5a0374a30d1b4df1faed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813579"
---
# <a name="functional-flow-for-smart-card"></a>智能卡的功能流

由于智能卡与 NFP 共享驱动程序，因此当智能卡接近时，NDEF 处理优先，使更高级别的服务能够在 NDEF 消息类型上运行，然后应用程序才能与卡通信。

![描述智能卡发现时 NDEF 消息的层次结构读取和写入的流程图。](images/smartcardfunctionalflow.png)

## <a name="related-topics"></a>相关主题

[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/_nfpdrivers)  
[智能卡 DDI 和命令参考](/previous-versions/dn905601(v=vs.85))
