---
title: NFC 类扩展可扩展性模型
description: NFC 类扩展驱动程序开发人员可以添加特定于芯片组的 NCI 专有扩展插件未涵盖的 NCI 规范。
ms.assetid: 8CCCE7BF-595A-4F30-9924-B5BD45D6137F
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3b2a5c47ed8be8f9066446ec7ff5acf231bbf2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370514"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC 类扩展可扩展性模型


NFC 类扩展驱动程序的主要目的是向客户端驱动程序提供灵活地添加特定于芯片组的 NCI 专有扩展插件未涵盖的 NCI 规范。

若要解决此问题，NFC 类扩展驱动程序，提供了客户端驱动程序提供对这些 NCI 供应商扩展的支持包括但不是限于 NCI 定义 RF 协议的专有实现的多个扩展点若要配置为低能耗模式和固件参数的其他特定于芯片集的配置的 NFC 控制器和其他操作的特定于芯片组的 NCI 命令。

NFC 类扩展驱动程序的 NFC 客户端驱动程序提供了三个扩展点：

-   [序列处理](sequence-handling.md)
-   RF 协议和接口可扩展性
-   NCI 数据包处理

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
