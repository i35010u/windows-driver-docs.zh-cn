---
title: NFC 体系结构
description: 下面进一步显示了 Windows 上 NFC 堆栈的高级体系结构示意图。 NFC UMDF 驱动程序将实现此规范中所述的 DDIs。
ms.assetid: 0FA2BE92-05E1-40D1-AD1D-AE9ADF425E67
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e3ca359cba07b01e056dffe1f2670872be9eb5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841697"
---
# <a name="nfc-architecture"></a>NFC 体系结构


下面进一步显示了 Windows 上 NFC 堆栈的高级体系结构示意图。 NFC UMDF 驱动程序将实现此规范中所述的 DDIs。

-   [近现场附近 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) –为邻近消息传递提供发布/订阅功能，包括对等互连消息的对等交换以及从 NFC 标记接收和写入数据。
-   [安全元素 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) –提供对连接到 NFC 控制器的安全元素（SEs）的访问权限，允许向外部读取器公开安全元素，并允许将事件从 NFCC 和 applet 转发到更高层，还提供用于配置和管理 NFC 芯片侦听模式路由配置的访问权限。 它还提供了在侦听模式下接收和传输 ISO/IEC 7816-4 Apdu 到远程设备的访问权限。
-   [智能卡 DDI](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85)) –提供低级别的访问权限，以便与智能卡进行交互，如侦听卡到达/出发的能力，允许将请求传输到智能卡，并允许检索智能卡信息。
-   [无线电管理 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) –提供控制面板（CPL）应用程序的访问权限，以设置邻近感应（P2P 和读取器/写入器模式）和安全元素（卡仿真模式）的无线电状态。

![描述 NFC 堆栈的流程图，从顶级应用程序开始，用户模式服务，UMDF 驱动程序，内核模式，最后是硬件。](images/nfcarchitecture.png)

 

 
## <a name="related-topics"></a>相关主题
 [NFC 设备驱动程序接口 (DDI) 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
 
