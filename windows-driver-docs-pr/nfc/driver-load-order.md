---
title: NFC 驱动程序加载顺序
description: ACPI 创建用于表示 NFCC，即插即用设备节点时针对 NFC 客户端提供驱动程序.inf 匹配和安装该设备节点。
ms.assetid: 8094B525-A4A1-42D2-8D1F-4B32D77418E3
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b3305bec5c9b69d4e846306244be1cc42261eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375232"
---
# <a name="nfc-driver-load-order"></a>NFC 驱动程序加载顺序


ACPI 创建用于表示 NFCC，即插即用设备节点时针对 NFC 客户端提供驱动程序.inf 匹配和安装该设备节点。 NFC 客户端驱动程序将在其 AddDevice 例程，初始化类扩展，这将允许由 Microsoft 提供的 NFC 类扩展 (NfcCx.dll) 加载，并允许本身的上半部分 NFC 类必须实现处理任何 I/O 队列的安装程序扩展驱动程序。 下图说明了驱动程序加载机制。

![驱动程序加载顺序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

