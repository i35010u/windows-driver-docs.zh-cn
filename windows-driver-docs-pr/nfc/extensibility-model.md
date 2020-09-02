---
title: NFC 类扩展扩展性模型
description: NFC 类扩展驱动程序允许开发人员添加 NCI 规范未涵盖的特定于芯片组的 NCI 专用扩展。
ms.assetid: 8CCCE7BF-595A-4F30-9924-B5BD45D6137F
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d847dc06732c0a9471f2a5d6e20c9692b962f06
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382019"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC 类扩展扩展性模型


NFC 类扩展驱动程序的主要用途是提供客户端驱动程序，以灵活地添加 NCI 规范未涵盖的特定于芯片组的 NCI 专用扩展。

为满足这一目的，NFC 类扩展驱动程序为客户端驱动程序提供了多个扩展点，以支持这些 NCI 的供应商扩展，这些扩展插件包括但不限于非 NCI 定义射频协议的专有实现、特定于芯片组的 NCI 命令，用于为低功率模式和其他特定于芯片组的固件参数配置配置 NFC 控制器等。

NFC 类扩展驱动程序为 NFC 客户端驱动程序提供了三个扩展点：

-   [序列处理](sequence-handling.md)
-   RF 协议和接口扩展性
-   NCI 数据包处理

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)