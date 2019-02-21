---
title: NFC 类扩展可扩展性模型
description: NFC 类扩展驱动程序开发人员可以添加特定于芯片组的 NCI 专有扩展插件未涵盖的 NCI 规范。
ms.assetid: 8CCCE7BF-595A-4F30-9924-B5BD45D6137F
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 558e002b770362d7c9e2f96e5ca480905e476261
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556135"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC 类扩展可扩展性模型


NFC 类扩展驱动程序的主要目的是向客户端驱动程序提供灵活地添加特定于芯片组的 NCI 专有扩展插件未涵盖的 NCI 规范。

若要解决此问题，NFC 类扩展驱动程序，提供了客户端驱动程序提供对这些 NCI 供应商扩展的支持包括但不是限于 NCI 定义 RF 协议的专有实现的多个扩展点若要配置为低能耗模式和固件参数的其他特定于芯片集的配置的 NFC 控制器和其他操作的特定于芯片组的 NCI 命令。

NFC 类扩展驱动程序的 NFC 客户端驱动程序提供了三个扩展点：

-   [序列处理](sequence-handling.md)
-   RF 协议和接口可扩展性
-   NCI 数据包处理

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  
