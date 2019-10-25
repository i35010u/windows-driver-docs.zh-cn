---
title: NFC 类扩展扩展性模型
description: NFC 类扩展驱动程序允许开发人员添加 NCI 规范未涵盖的特定于芯片组的 NCI 专用扩展。
ms.assetid: 8CCCE7BF-595A-4F30-9924-B5BD45D6137F
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c406505aa705ac342e59dafea05acfa5b27442c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843418"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC 类扩展扩展性模型


NFC 类扩展驱动程序的主要用途是提供客户端驱动程序，以灵活地添加 NCI 规范未涵盖的特定于芯片组的 NCI 专用扩展。

为了适应这种情况，NFC 类扩展驱动程序为客户端驱动程序提供了多个扩展点，以支持这些 NCI 供应商扩展，这些扩展包括但不限于非 NCI 定义射频协议的专用实现。芯片组特定的 NCI 命令，用于为低能耗模式和其他特定于芯片组的固件参数配置配置 NFC 控制器。

NFC 类扩展驱动程序为 NFC 客户端驱动程序提供了三个扩展点：

-   [序列处理](sequence-handling.md)
-   RF 协议和接口扩展性
-   NCI 数据包处理

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
