---
title: 功能流
description: 智能卡发现后对 NDEF 消息进行分层读取和写入的流程图和简短说明。
ms.assetid: 7B4B4902-FD16-4C9B-BB54-A1D6EFCAE9DB
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 312e39dda227ad87ec774808337f6ab4e100b470
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384821"
---
# <a name="functional-flow"></a>功能流


由于智能卡与 NFP 共享驱动程序，因此当智能卡接近时，NDEF 处理优先，使更高级别的服务能够在 NDEF 消息类型上运行，然后应用程序才能与卡通信。

![描述智能卡发现时 NDEF 消息的层次结构读取和写入的流程图。](images/smartcardfunctionalflow.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[智能卡 DDI 和命令参考](/previous-versions/dn905601(v=vs.85))