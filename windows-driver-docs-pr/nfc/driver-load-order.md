---
title: NFC 驱动程序加载顺序
description: 当 ACPI 创建设备节点以表示 NFCC 时，PnP 将与 NFC 客户端驱动程序（如果为该设备节点）匹配。
ms.assetid: 8094B525-A4A1-42D2-8D1F-4B32D77418E3
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d747ed4138f98573c157f644ccd0f83d5229d518
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384861"
---
# <a name="nfc-driver-load-order"></a>NFC 驱动程序加载顺序


当 ACPI 创建设备节点以表示 NFCC 时，PnP 将与 NFC 客户端驱动程序（如果为该设备节点）匹配。 NFC 客户端驱动程序将在其 AddDevice 例程期间初始化类扩展，这将允许 Microsoft 提供的 NFC 类扩展 ( # A0) 负载，并让自己设置其在 NFC 类扩展驱动程序的顶层上必须实现的任何 i/o 队列处理。 下图说明了驱动程序加载机制。

![驱动程序加载顺序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)