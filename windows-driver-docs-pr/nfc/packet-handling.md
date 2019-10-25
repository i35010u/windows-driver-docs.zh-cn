---
title: NCI 数据包处理
description: 在某些情况下，nfc CX 定义的序列可能不足以使 NFC 客户端驱动程序添加其自定义逻辑。
ms.assetid: 48BD5100-A1D4-4844-B53A-DAC73FDBB089
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 668e3ca49c98070b6e2f65a77084712c354001e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831569"
---
# <a name="nci-packet-handling"></a>NCI 数据包处理


在某些情况下，nfc CX 定义的序列可能不足以使 NFC 客户端驱动程序添加其自定义逻辑。 在这些情况下，因为通过 NFC 客户端驱动程序（该驱动程序处理与传输层的交互）将 NFC CX 与 NFC 控制器交换所有 NCI 数据包，这使 NFC 客户端驱动程序可以在CX 和 NFCC 交换的标准 NCI 数据包。 但是，当 NFC 客户端驱动程序利用此扩展点以及在 "序列扩展性" 部分中指定的要求（1）和（2）时，它必须满足以下要求：

-   当这些附加的 NCI 数据包的交换完成后，NFC 客户端驱动程序必须通过[**NfcCxNciReadNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)回调发送与 NFC CX 发送的 NCI 命令相关联的响应和通知。

-   由于每通道流控制是在 NFC CX 的逻辑通道管理中执行的，因此 NFC 客户端驱动程序不应执行影响此的任何逻辑。 因此，建议 NFC 客户端驱动程序不会在不知道的情况下，在由 CX 打开的逻辑通道上发送任何其他数据包。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

