---
title: NFC 类扩展
description: 本部分介绍 NFC 类扩展 (CX) 和 NFC 客户端驱动程序之间的接口。
ms.assetid: 64599C5E-7E72-4712-B733-24C078919B84
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
- CX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ff8f74e80942dc8d8578e9921cf23e9b7995a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378869"
---
# <a name="nfc-class-extension-cx-design-guide"></a>NFC 类扩展 (CX) 设计指南


本部分介绍 NFC 类扩展 (CX) 和 NFC 客户端驱动程序之间的接口。 NFC CX 驱动程序实现所有 NFC 设备驱动程序接口和标准 NFC 协议和格式根据*NFC 论坛 NFC 控制器接口 (NCI) 的技术规范*。

NFC 客户端驱动程序负责传输层进行交互以及对优化 NFC 控制器才能发挥作用供应商定义任何非标准扩展的支持。

NFC 类扩展驱动程序实现所有标准 NFC 论坛标记 （T1T、 T2T、 T3T、 ISO DEP） 和 P2P （LLCP 和 SNEP） 协议和 RF 管理基于 NCI 核心规范。 类扩展驱动程序实现了与 NFC 控制器、 安全元素和远程 RF 终结点进行交互的所有 Windows 定义的设备驱动程序接口。

这些主题描述的体系结构和之间 NFC 类扩展驱动程序由 Microsoft 和 NFC 客户端驱动程序提供的相应的芯片组制造商提供的公共接口。 NFC CX 驱动程序设计为支持来自各个制造商的 NFC 芯片集，并启用制造商在差异化目的其 NFC 客户端驱动程序中实现非 NCI 标准功能。

## <a name="nfc-driver-ddi"></a>NFC 驱动程序 DDI
Windows 定义 NFC 驱动程序由 NFC CX 驱动程序实现的 DDI 如下：

-   [邻近 DDI 附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)
-   [NFC 安全元素管理 DDI](https://msdn.microsoft.com/library/windows/hardware/dn905485)
-   [非接触式智能卡访问的智能卡 DDI](https://msdn.microsoft.com/library/windows/hardware/dn905601)
-   [NFC 射频硬件管理 DDI](https://msdn.microsoft.com/library/windows/hardware/dn905577)
-   DTA DDI NFC 论坛认证

## <a name="nfc-forum-specifications"></a>NFC 论坛规范
以下是由 NFC CX 驱动程序实现的 NFC 论坛规范：  

-   NFC 控制器接口、 NCI 1.0 规范
-   NFC 数据交换格式 NDEF
-   NFC 论坛键入 1 到 4 标记
-   逻辑链接控制协议、 LLCP 1.1 规范
-   简单 NDEF 交换协议、 SNEP 1.0 规范
-   ISO/IEC 15693

## <a name="supported-nfc-smart-cards-and-tags"></a>支持的 NFC 智能卡和标记
以下是 NFC 智能卡和 NFC CX 驱动程序支持的标记：  

-   MIFARE 经典系列
-   MIFARE Ultralight 系列
-   MIFARE DESFire 系列
-   FeliCa 系列
-   包装盒/简称 Topaz 系列
-   泛型 ISO 15693 标记
-   Thinfilm NFC 条形码 (Kovio)



## <a name="in-this-section"></a>本节内容


-   [术语表](glossary.md)
-   [体系结构](architecture.md)
-   [NFC 堆栈体系结构](nfc-stack-architecture.md)
-   [驱动程序加载顺序](driver-load-order.md)
-   [类扩展接口](nfc-class-extension-interface.md)
-   [类扩展状态机](nfc-class-extension-state-machine.md)
-   [扩展性模型](extensibility-model.md)
-   [可配置性](configurability.md)
-   [错误处理](error-handling.md)
-   [电源状态](power-states.md)
-   [NFC 客户端驱动程序电源管理要求](nfc-client-driver-power-management-requirements.md)
-   [日志记录](logging.md)
-   [保留的数据](persisted-data.md)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_nfpdrivers/)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/)  
