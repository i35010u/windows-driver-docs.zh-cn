---
title: NFC 驱动程序加载顺序
description: 当 ACPI 创建设备节点以表示 NFCC 时，PnP 将与 NFC 客户端驱动程序（如果为该设备节点）匹配。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1753ab689615124a2ae09dcf0ea773c0dad55350
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813599"
---
# <a name="nfc-driver-load-order"></a>NFC 驱动程序加载顺序


当 ACPI 创建设备节点以表示 NFCC 时，PnP 将与 NFC 客户端驱动程序（如果为该设备节点）匹配。 NFC 客户端驱动程序将在其 AddDevice 例程期间初始化类扩展，这将允许 Microsoft 提供的 NFC 类扩展 ( # A0) 负载，并让自己设置其在 NFC 类扩展驱动程序的顶层上必须实现的任何 i/o 队列处理。 下图说明了驱动程序加载机制。

![驱动程序加载顺序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
