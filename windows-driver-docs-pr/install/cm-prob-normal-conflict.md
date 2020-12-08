---
title: CM_PROB_NORMAL_CONFLICT
description: CM_PROB_NORMAL_CONFLICT
keywords:
- CM_PROB_NORMAL_CONFLICT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cc0a83670e7121b50f70bb31a24bc54a7214d56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783095"
---
# <a name="code-12---cm_prob_normal_conflict"></a>代码 12 - CM_PROB_NORMAL_CONFLICT

此设备管理器错误消息表明，为两个设备分配了相同的 i/o 端口、相同的中断或相同的 DMA 通道， (BIOS、操作系统或这两种) 的组合。

## <a name="error-code"></a>错误代码

12

### <a name="display-message"></a>显示消息

"此设备找不到足够的可用资源。  (代码 12) 

"如果要使用此设备，则需要禁用此系统上的另一台设备。"

### <a name="recommended-resolution"></a>推荐的解决方案

[使用设备管理器](using-device-manager.md) 确定冲突源并解决冲突。 有关如何解决设备冲突的详细信息，请参阅有关如何使用设备管理器的帮助信息。

如果 BIOS 未将足够的资源分配给设备，也会出现此错误消息。 例如，如果 BIOS 未将中断分配到 USB 控制器，因为)  (MP 的多处理器规范无效，则会显示此消息。
