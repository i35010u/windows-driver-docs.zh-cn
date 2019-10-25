---
title: NFC 驱动程序加载顺序
description: 当 ACPI 创建设备节点以表示 NFCC 时，PnP 将与 NFC 客户端驱动程序（如果为该设备节点）匹配。
ms.assetid: 8094B525-A4A1-42D2-8D1F-4B32D77418E3
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6912d3f22c9a2fb30913f681d318b7b68655ef34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843422"
---
# <a name="nfc-driver-load-order"></a>NFC 驱动程序加载顺序


当 ACPI 创建设备节点以表示 NFCC 时，PnP 将与 NFC 客户端驱动程序（如果为该设备节点）匹配。 NFC 客户端驱动程序将在其 AddDevice 例程期间初始化类扩展，这将允许 Microsoft 提供的 NFC 类扩展（NfcCx）加载，并让自身设置为 NFC 类的上半部分实现的任何 i/o 队列处理扩展驱动程序。 下图说明了驱动程序加载机制。

![驱动程序加载顺序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

