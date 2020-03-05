---
title: CM_PROB_NORMAL_CONFLICT
description: CM_PROB_NORMAL_CONFLICT
ms.assetid: 18c5ca02-0a4c-4a0e-8b33-5c685a73d4c8
keywords:
- CM_PROB_NORMAL_CONFLICT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8dabe519441bf0a0f77196ea39b249e51284268
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279511"
---
# <a name="code-12---cm_prob_normal_conflict"></a>代码 12-CM_PROB_NORMAL_CONFLICT

此设备管理器错误消息表明，为两个设备分配了相同的 i/o 端口、相同的中断或相同的 DMA 通道（由 BIOS、操作系统或二者的组合）。

## <a name="error-code"></a>错误代码

12

### <a name="display-message"></a>显示消息

"此设备找不到足够的可用资源。 （代码12）

"如果要使用此设备，则需要禁用此系统上的另一台设备。"

### <a name="recommended-resolution"></a>建议的解决方法

[使用设备管理器](using-device-manager.md)确定冲突源并解决冲突。 有关如何解决设备冲突的详细信息，请参阅有关如何使用设备管理器的帮助信息。

如果 BIOS 未将足够的资源分配给设备，也会出现此错误消息。 例如，如果由于多处理器规范（MPS）表无效，BIOS 不将中断分配到 USB 控制器，则会显示此消息。
