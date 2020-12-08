---
title: NFCEE 发现序列
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: NFC CX 的相关信息，提供两种操作模式以支持不同的 NFCEE 管理实现。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2660fd42603a592236550c87d4b2a1c15b2eff09
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813499"
---
# <a name="nfcee-discovery-sequence"></a>NFCEE 发现序列


由于 NCI 1.0 规范的限制，芯片组制造商具有不同的 NFCEE 管理实现。 为了支持这些不同的实现，NFC CX 提供了两种操作模式：

-   **标准 NCI 模式** –在此模式下，NFC CX 允许 NFCC 报告所有 NFCEEs 的单一 HCI 网络。 对于其他 NFCEEs，不存在单独的 NFCEE \_ 发现 \_ contoso.ntf。 不过，NFC CX 在此配置中支持单个 NFCEE。 此模式的扩展。如果 NFCC 报告每个 NFCEE 的 HCI 网络，NFC CX 将选取第一个并放弃其余。

-   **非标准 NCI 模式** –在此模式下，NFC CX 允许 NFCC 报告所有 NFCEEs 的单一 HCI 网络。 此外，它还会在其 NFCEE 发现 Contoso.ntf 中单独报告网络上的子 NFCEEs \_ \_ 。 但是，NFC CX 有另外两个要求来支持此配置。 NFCEE 发现 RSP 中报告的 NFCEEs 数量 \_ \_ 很大程度上包括子 NFCEEs。 另外，子 NFCCs 的 NFCEEIDs 必须与 HCI 主机 Id 匹配 (HCI 标准版要求 UICC 主机 ID) 为0x2。

此配置中的大多数 NFCCs 实现仅在其 NFCEE 发现 RSP 中报告 HCI 网络 NFCEEID \_ \_ 。 不过，由于 NFC CX 并不知道实际数量，因此无法确定发现过程何时完成。 NFC 客户端驱动程序通常有一种专用机制来了解要报告的其他 NFCEEs。 因此，在其传输处理中，NFC 客户端驱动程序可以对响应中的其他 NFCEEs 实现一种小型解决方法来满足此要求。

![非标准 nci nfcee 发现序列](images/nonstandardnci-nfceediscoverysequence.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
