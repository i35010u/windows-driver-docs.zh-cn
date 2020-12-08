---
title: NFC 类扩展扩展性模型
description: NFC 类扩展驱动程序允许开发人员添加 NCI 规范未涵盖的特定于芯片组的 NCI 专用扩展。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94ecef0e42563198da3d13534913b000fed0beb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813587"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC 类扩展扩展性模型

NFC 类扩展驱动程序的主要用途是提供客户端驱动程序，以灵活地添加 NCI 规范未涵盖的特定于芯片组的 NCI 专用扩展。

为满足这一目的，NFC 类扩展驱动程序为客户端驱动程序提供了多个扩展点，以支持这些 NCI 的供应商扩展，这些扩展插件包括但不限于非 NCI 定义射频协议的专有实现、特定于芯片组的 NCI 命令，用于为低功率模式和其他特定于芯片组的固件参数配置配置 NFC 控制器等。

NFC 类扩展驱动程序为 NFC 客户端驱动程序提供了三个扩展点：

- [序列处理](sequence-handling.md)
- RF 协议和接口扩展性
- NCI 数据包处理

## <a name="related-topics"></a>相关主题

[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/_nfpdrivers)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/nfccx)
