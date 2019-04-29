---
title: CM_PROB_NORMAL_CONFLICT
description: CM_PROB_NORMAL_CONFLICT
ms.assetid: 18c5ca02-0a4c-4a0e-8b33-5c685a73d4c8
keywords:
- CM_PROB_NORMAL_CONFLICT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46a8c7c5e4cb40f08e563d03d5570268c96da4a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355761"
---
# <a name="cmprobnormalconflict"></a>CM_PROB_NORMAL_CONFLICT

此函数保留供系统使用。

相同的 I/O 端口、 同一中断端口或同一个 DMA 通道 （不论是通过 BIOS、 操作系统或两者的组合） 分配了两个设备。

## <a name="error-code"></a>错误代码

12

### <a name="display-message"></a>显示消息

"此设备找不到可以使用足够可用资源。 （代码 12）

"如果您想要使用此设备，你将需要禁用其中一个此系统上的其他设备。"

### <a name="recommended-resolution"></a>建议的解决方法

[使用设备管理器](using-device-manager.md)来确定冲突的根源并解决该冲突。 有关如何解决设备冲突的详细信息，请参阅有关如何使用设备管理器的帮助信息。

如果 BIOS 没有分配到设备的足够资源，也会出现此错误消息。 例如，如果 BIOS 不会由于无效的多处理器规范 (MPS) 表分配到 USB 控制器中断，则将显示此消息。
