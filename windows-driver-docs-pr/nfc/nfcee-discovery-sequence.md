---
title: NFCEE 发现序列
ms.assetid: F6894EFD-4140-490B-B0BB-1A9BDA4DCECE
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
description: NFC CX，提供了两种操作以支持不同的实现 NFCEE 管理模式有关的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ef73466084e3d016cf644a45c29c6a0ee88a2dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520711"
---
# <a name="nfcee-discovery-sequence"></a>NFCEE 发现序列


由于 NCI 1.0 规范的限制，芯片组制造商具有 NFCEE 管理的不同实现。 若要支持这些不同的实现，NFC CX 提供了两种操作模式：

-   **标准 NCI 模式**– 在此模式下，NFC CX 允许 NFCC 来报告单个 HCI 网络，以便所有 NFCEEs。 没有单独 NFCEE\_发现\_其他 NFCEEs 的 NTF。 NFC CX，但是，限制为在此配置中支持单一 NFCEE。 此模式下，如果 NFCC 报告每 NFCEE，NFC CX HCI 网络的扩展将选择第一个，并丢弃其余部分。

-   **非标准 NCI 模式**– 在此模式下，NFC CX 允许 NFCC 来报告单个 HCI 网络，以便所有 NFCEEs。 此外，它报告在其 NFCEE 中单独网络上子 NFCEEs\_发现\_NTF。 但是，NFC CX 已在两个额外要求，以支持此配置。 NFCEE 中报告的 NFCEEs 数\_发现\_RSP 得包括子 NFCEEs。 此外，子 NFCCs NFCEEIDs 必须匹配 HCI 主机 Id （HCI 标准要求要 0x2 UICC 主机 ID）。

在此配置中的 NFCCs 的大多数实现报告仅在 HCI 网络中其 NFCEE NFCEEID\_发现\_RSP。 但是，由于 NFC CX 不知道的实际数目，其无法确定在发现过程完成时。 NFC 客户端驱动程序通常具有一种知道会报告其他 NFCEEs 的专有机制。 因此，NFC 客户端驱动程序可以在处理实现其传输到其他解决方法在响应中的其他 NFCEEs 来满足此要求。

![非标准 nci nfcee 发现序列](images/nonstandardnci-nfceediscoverysequence.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  
