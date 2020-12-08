---
title: 错误处理
description: 本主题讨论 NFC 客户端的错误处理要求。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9de1f5c4487c2a3c69dbaf98e1dce37fffa5a22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813591"
---
# <a name="error-handling"></a>错误处理


本主题讨论 NFC 客户端的错误处理要求。

-   NFC 客户端驱动程序负责在对控制器执行写入请求时遇到错误时，通知 NFC CX。 接收到错误状态时，NFC CX 会执行重试、恢复或进入错误状态。

-   完成序列调用时，NFC 客户端驱动程序可能会报告错误。 NFC CX 会输入恢复或输入错误状态，具体取决于当前状态。

-   NFCC 遇到崩溃时，预期会将核心 \_ 重置 \_ contoso.ntf 发送到主机。 接收核心 \_ 重置 contoso.ntf 的 NFC CX \_ 会执行相应的恢复。

-   当客户端检测到无法恢复的错误时，它可以通知 NFC CX 通过 HostActionRestart 执行完整的驱动程序重启，或请求它使用 HostActionUnload 卸载驱动程序。

-   如果 NFC 客户端需要触发用户模式故障 (例如，检测内存损坏) ，则 NFC 客户端驱动程序将使用 WDF 验证器 Api 来使用 NFC 客户端驱动程序保留范围内的 bug 检查代码触发崩溃 (有关详细) 信息，请参阅 NfcCxBugCodes。 由于默认情况下启用了进程共享，因此，仅当绝对需要时 NFC 客户端驱动程序才使用此机制是非常重要的，否则，它可能会在 WUDF 驱动程序主机进程中关闭其他驱动程序。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
