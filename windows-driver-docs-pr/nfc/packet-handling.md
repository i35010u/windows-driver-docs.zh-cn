---
title: NCI 数据包处理
description: 在某些情况下，nfc CX 定义的序列可能不足以使 NFC 客户端驱动程序添加其自定义逻辑。
ms.assetid: 48BD5100-A1D4-4844-B53A-DAC73FDBB089
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa4c4fdb430eca23783368486f5801dcae007d76
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382455"
---
# <a name="nci-packet-handling"></a>NCI 数据包处理


在某些情况下，nfc CX 定义的序列可能不足以使 NFC 客户端驱动程序添加其自定义逻辑。 在这些情况下，因为所有 NCI 数据包都通过 nfc 客户端驱动程序与 NFC 控制器交换，而 nfc 客户端驱动程序 (处理传输层) 的接口，这使 NFC 客户端驱动程序可以在 CX 和 NFCC 交换的标准 NCI 数据包之间注入附加的 NCI 数据包。 但是，当 NFC 客户端驱动程序利用此扩展点时，除了在序列扩展性部分中指定的要求 (1) 和 (2) ，NFC 客户端驱动程序必须满足以下要求：

-   当这些附加的 NCI 数据包的交换完成后，NFC 客户端驱动程序必须通过 [**NfcCxNciReadNotification**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification) 回调发送与 NFC CX 发送的 NCI 命令相关联的响应和通知。

-   由于每通道流控制是在 NFC CX 的逻辑通道管理中执行的，因此 NFC 客户端驱动程序不应执行影响此的任何逻辑。 因此，建议 NFC 客户端驱动程序不会在不知道的情况下，在由 CX 打开的逻辑通道上发送任何其他数据包。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)