---
title: P2P RF 数据交换序列
description: 下图说明了 StateRfDiscovered 和 StateRfDataXchg 的状态顺序。
ms.assetid: FF77D322-47AE-412C-9924-110FB9E8F9F5
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339531ecf27a1ba8b6904b8ea8118fabb31853c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845266"
---
# <a name="p2p-rf-data-exchange-sequence"></a>P2P RF 数据交换序列


下图说明了 StateRfDiscovered 和 StateRfDataXchg 的状态顺序。 请注意，NFC CX 要求 NFCC 支持用于 P2P 处理的 NFC DEP RF 接口。 StateRfDiscovered 的转换在 RF 接口激活之后发生。 对于多个远程终结点或 StateRfDiscovery 中的多个协议，NFC CX 选择单个终结点。 NFC-dep over ISO 的首选项是在 NFC CX 中实现的，旨在提高互操作性。 StateRfDiscovered 是一个过渡状态，其中 NFC CX 检查远程设备是否支持 LLCP。 对于 P2P 模式，StateRfDataXchg 划分为以下操作顺序：检查远程设备是否支持 LLCP、绑定、侦听和接受默认 SNEP 服务器上的连接，并打开与远程默认 SNEP 服务器的连接。 驱动程序使用 SNEP 命令从应用程序层交换任何可用的 NDEF 消息请求。

![nfc-dep rf 数据交换序列](images/nfc-dep-rfdataexchangesequence.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

