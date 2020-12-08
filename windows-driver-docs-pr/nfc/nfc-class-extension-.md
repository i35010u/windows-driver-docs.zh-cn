---
title: NFC 类扩展
description: 本部分介绍 NFC 类扩展 (CX) 和 NFC 客户端驱动程序之间的接口。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
- CX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03124893baec2b8e7abf08525aa4983947fadf5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813535"
---
# <a name="nfc-class-extension-cx-design-guide"></a>NFC 类扩展 (CX) 设计指南


本部分介绍 NFC 类扩展 (CX) 和 NFC 客户端驱动程序之间的接口。 NFC CX 驱动程序实现所有 NFC 设备驱动程序接口和标准 NFC 协议，并基于 *Nfc 论坛 Nfc 控制器接口 (NCI) 技术规范*。

NFC 客户端驱动程序负责传输层交互，并支持任何非标准供应商定义的扩展，以优化 NFC 控制器的功能。

NFC 类扩展驱动程序实现了所有标准 NFC 论坛标记 (T1T、T2T、T3T、ISO-DEP) 和 P2P (LLCP 和 SNEP) 协议，以及基于 NCI 核心规范的 RF 管理。 类扩展驱动程序实现所有 Windows 定义的设备驱动程序接口，以与 NFC 控制器、安全元素和远程 RF 终结点进行交互。

这些主题介绍了 Microsoft 提供的 NFC 类扩展驱动程序与相应芯片组制造商提供的 NFC 客户端驱动程序之间的体系结构和公共接口。 NFC CX 驱动程序设计为支持来自各种制造商的 NFC 芯片组，并使制造商可以在其 NFC 客户端驱动程序中实现非 NCI 标准功能，目的是出于区分目的。

## <a name="nfc-driver-ddi"></a>NFC 驱动程序 DDI
以下是由 NFC CX 驱动程序实现的 Windows 定义的 NFC 驱动程序 DDI：

-   [近现场邻近 DDI](/windows-hardware/drivers/ddi/index)
-   [NFC 安全元素管理 DDI](/windows-hardware/drivers/ddi/index)
-   [用于 contactless 智能卡访问的智能卡 DDI](/previous-versions/dn905601(v=vs.85))
-   [NFC 无线电管理 DDI](/windows-hardware/drivers/ddi/index)
-   适用于 NFC 论坛认证的 DTA DDI

## <a name="nfc-forum-specifications"></a>NFC 论坛规范
以下是 NFC CX 驱动程序实现的 NFC 论坛规范：  

-   NFC 控制器接口，NCI 1.0 规范
-   NFC 数据交换格式，NDEF
-   NFC 论坛类型1-4 标记
-   逻辑链接控制协议，LLCP 1.1 规范
-   简单 NDEF Exchange 协议，SNEP 1.0 规范
-   ISO/IEC 15693

## <a name="supported-nfc-smart-cards-and-tags"></a>支持的 NFC 智能卡和标记
以下是 NFC CX 驱动程序支持的 NFC 智能卡和标记：  

-   MIFARE 经典系列
-   MIFARE Ultralight 系列
-   MIFARE DESFire 系列
-   FeliCa 系列
-   宝石/Topaz 系列
-   一般 ISO 15693 标记
-   Thinfilm NFC 条形码 (Kovio) 



## <a name="in-this-section"></a>在本节中


-   [术语表](glossary.md)
-   [体系结构](architecture.md)
-   [NFC 堆栈体系结构](nfc-stack-architecture.md)
-   [驱动程序加载顺序](driver-load-order.md)
-   [类扩展接口](nfc-class-extension-interface.md)
-   [类扩展状态机](nfc-class-extension-state-machine.md)
-   [扩展性模型](extensibility-model.md)
-   [可配置性](configurability.md)
-   [错误处理](error-handling.md)
-   [Power 状态](power-states.md)
-   [NFC 客户端驱动程序电源管理要求](nfc-client-driver-power-management-requirements.md)
-   [Logging](logging.md)
-   [持久保留的数据](persisted-data.md)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/_nfpdrivers/)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/nfccx/)
