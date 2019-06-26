---
title: NFC 体系结构
description: Windows 上的 NFC 堆栈的高级体系结构关系图显示了下面将进一步。 NFC UMDF 驱动程序将实现此规范中所述 DDIs。
ms.assetid: 0FA2BE92-05E1-40D1-AD1D-AE9ADF425E67
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382be44e5d0b65bb3235b1d2eb3fd2efa49a12c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383579"
---
# <a name="nfc-architecture"></a>NFC 体系结构


Windows 上的 NFC 堆栈的高级体系结构关系图显示了下面将进一步。 NFC UMDF 驱动程序将实现此规范中所述 DDIs。

-   [附近字段邻近 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) – 提供邻近和消息传递，其中包括对等交换邻近消息和接收从 NFC 标记写入数据的发布/订阅功能。
-   [保护元素 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) – 提供枚举安全元素 (SEs) 附加到 NFC 控制器的访问权限，允许向外部读者公开安全元素并允许将从 NFCC 和小程序的事件转发到较高的层，以及提供配置和管理 NFC 芯片侦听模式的路由配置的访问权限。 它还提供访问用于接收和发送 ISO/IEC 7816 4 Apdu 在侦听模式下与远程设备。
-   [智能卡 DDI](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85)) – 提供与智能卡等功能来侦听卡到达/出发进行交互的低级别访问权限，允许请求传输到智能卡中，并允许智能卡信息要检索。
-   [单选管理 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) – 提供有关要设置的邻近性 （P2P 和读取器/编写器模式） 和安全元素 （卡仿真模式） 的单选状态的控件面板 (CPL) 应用程序的访问。

![流程图描述 NFC 堆栈从底部从应用程序开始在顶部，用户模式服务，UMDF 驱动程序、 内核模式，然后硬件。](images/nfcarchitecture.png)

 

 
## <a name="related-topics"></a>相关主题
 [NFC 设备驱动程序接口 (DDI) 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
 
