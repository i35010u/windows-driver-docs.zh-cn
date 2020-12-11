---
title: NFC 体系结构
description: 下面进一步显示了 Windows 上 NFC 堆栈的高级体系结构示意图。 NFC UMDF 驱动程序将实现此规范中所述的 DDIs。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df92c8e70a29e279d9ff6a48a5bc2f44667398b2
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091206"
---
# <a name="nfc-architecture"></a>NFC 体系结构


下面进一步显示了 Windows 上 NFC 堆栈的高级体系结构示意图。 NFC UMDF 驱动程序将实现此规范中所述的 DDIs。

-   [近现场附近 DDI](/windows-hardware/drivers/ddi/_nfpdrivers/#functions) –为邻近消息传递提供发布/订阅功能，包括对等互连消息的对等交换以及从 NFC 标记接收和写入数据。
-   [安全元素 DDI](/windows-hardware/drivers/ddi/_nfpdrivers/#functions) –提供访问权限以枚举附加到 NFC 控制器 (SEs) 的安全元素，允许向外部读取器公开安全元素，并允许将事件从 NFCC 和小程序转发到更高层，还提供了配置和管理 NFC 芯片侦听模式路由配置的访问权限。 它还提供了在侦听模式下接收和传输 ISO/IEC 7816-4 Apdu 到远程设备的访问权限。
-   [智能卡 DDI](/previous-versions/dn905601(v=vs.85)) –提供低级别的访问权限，以便与智能卡进行交互，如侦听卡到达/出发的能力，允许将请求传输到智能卡，并允许检索智能卡信息。
-   [无线电管理 DDI](/windows-hardware/drivers/ddi/_nfpdrivers/#functions) –为控制面板 () CPL 提供访问权限，以设置邻近性 (P2P 和读取器/写入器模式的无线电状态) 和安全元素 (卡仿真模式) 。

![描述 NFC 堆栈的流程图，从顶级应用程序开始，用户模式服务，UMDF 驱动程序，内核模式，最后是硬件。](images/nfcarchitecture.png)

 

 
## <a name="related-topics"></a>相关主题
 [NFC 设备驱动程序接口 (DDI) 参考](/windows-hardware/drivers/ddi/index)  
