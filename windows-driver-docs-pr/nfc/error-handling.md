---
title: 错误处理
description: 本主题讨论错误处理 NFC 客户端的要求。
ms.assetid: 52376A1F-9ADD-4297-ADF9-A1EBF5714316
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 893154fc4afe84e60a0b9a98e2795dc433c1b85e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370526"
---
# <a name="error-handling"></a>错误处理


本主题讨论错误处理 NFC 客户端的要求。

-   NFC 客户端驱动程序负责执行到控制器的写入请求时遇到错误时通知 NFC CX。 NFC CX 在收到错误状态时将执行重试，并恢复，或进入错误状态。

-   完成序列调用时，NFC 客户端驱动程序可以报告错误。 根据当前状态，NFC CX 将进入恢复或输入错误状态。

-   当 NFCC 遇到故障时，预期它将发送一个核心\_重置\_NTF 到主机。 一旦收到核心 NFC CX\_重置\_NTF 将执行相应的恢复。

-   当客户端检测到无法恢复的错误时，它可以通知 NFC CX 操作通过 HostActionRestart 完整驱动程序重新启动，或请求它卸载使用 HostActionUnload 的驱动程序。

-   如果 NFC 客户端需要触发用户模式故障 （例如，检测内存损坏），则应 NFC 客户端驱动程序使用 WDF 验证程序 Api 来触发 NFC 客户端驱动程序 （请参阅使用的保留范围中的 bug 检查代码故障有关详细信息 NfcCxBugCodes.h)。 由于默认情况下启用了进程共享，务必 NFC 客户端驱动程序仅当绝对必要，否则它可能会使下 WUDF 驱动程序主机进程中的其他驱动程序使用此机制。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

