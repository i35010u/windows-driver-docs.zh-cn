---
title: 错误处理
description: 本主题讨论 NFC 客户端的错误处理要求。
ms.assetid: 52376A1F-9ADD-4297-ADF9-A1EBF5714316
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9bc4bacba5a1a850f7a75b96207f479d0561e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843415"
---
# <a name="error-handling"></a>错误处理


本主题讨论 NFC 客户端的错误处理要求。

-   NFC 客户端驱动程序负责在对控制器执行写入请求时遇到错误时，通知 NFC CX。 接收到错误状态时，NFC CX 会执行重试、恢复或进入错误状态。

-   完成序列调用时，NFC 客户端驱动程序可能会报告错误。 NFC CX 会输入恢复或输入错误状态，具体取决于当前状态。

-   当 NFCC 遇到故障时，预期会将核心\_重置\_CONTOSO.NTF 发送到主机。 接收核心\_重置\_CONTOSO.NTF 时，NFC CX 会执行相应的恢复。

-   当客户端检测到无法恢复的错误时，它可以通知 NFC CX 通过 HostActionRestart 执行完整的驱动程序重启，或请求它使用 HostActionUnload 卸载驱动程序。

-   如果 NFC 客户端需要触发用户模式故障（例如，检测内存损坏），则 NFC 客户端驱动程序应使用 WDF 验证器 Api，以使用 NFC 客户端驱动程序保留范围内的 bug 检查代码触发崩溃（请参阅NfcCxBugCodes 了解详细信息）。 由于默认情况下启用了进程共享，因此，仅当绝对需要时 NFC 客户端驱动程序才使用此机制是非常重要的，否则，它可能会在 WUDF 驱动程序主机进程中关闭其他驱动程序。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

