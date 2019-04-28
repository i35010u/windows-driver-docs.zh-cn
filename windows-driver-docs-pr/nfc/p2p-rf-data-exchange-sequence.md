---
title: P2P RF 数据交换序列
description: 下图展示了状态序列 StateRfDiscovered 和 StateRfDataXchg NFC DEP 协议。
ms.assetid: FF77D322-47AE-412C-9924-110FB9E8F9F5
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77af743b4f9469cc1e7db9048dd9242368301e7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348434"
---
# <a name="p2p-rf-data-exchange-sequence"></a>P2P RF 数据交换序列


下图展示了状态序列 StateRfDiscovered 和 StateRfDataXchg NFC DEP 协议。 请注意 NFC CX 要求 NFCC 来支持有关 P2P 处理 NFC DEP RF 接口。 RF 接口激活后发生的 StateRfDiscovered 转换。 在出现多个远程终结点或多个协议中 StateRfDiscovery，NFC CX 选择单个终结点。 NFC CX 改进互操作性的实现的 NFC DEP 通过 ISO DEP 首选项。 StateRfDiscovered 是 NFC CX 检查远程设备是否支持 LLCP 过渡状态。 为 P2P 模式 StateRfDataXchg 可划分为以下顺序操作： 检查，如果远程设备支持 LLCP、 绑定、 在侦听，并接受默认 SNEP 服务器上的连接打开与远程默认 SNEP 服务器的连接。 该驱动程序交换使用 SNEP 命令的应用程序层的任何可用 NDEF 邮件请求。

![nfc dep rf 数据交换序列](images/nfc-dep-rfdataexchangesequence.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

