---
title: 其他策略
description: 针对发布驱动程序的其他策略
ms.topic: article
ms.date: 09/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 59810d805d3bace1f1ac0b15c15c7414b1db8eb2
ms.sourcegitcommit: 10e87a839757a82aac9e10b657704ddc08aa8e08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97635252"
---
# <a name="overview-of-driver-policies"></a>驱动程序策略概述
驱动程序的外部测试和逐步推出可确保发布的驱动程序质量上乘，并且有助于限制驱动程序对 Windows 客户产生负面影响的几率。  为实现此目的，提供了一组用于确保质量的度量值。 此外，还提供了一些策略，可确保在生态系统中取得成功。

导致驱动程序提交遭到拒绝的一些现有策略包括：
* 面向 Windows 早期版本的驱动程序不能与适用于 Windows 10 的驱动程序包含在同一提交中。
* 某些设备类具有特定的 CHID 目标要求。 例如，“固件”和“显示器”类禁止使用 CHID。
* OEM 仅针对满足以下条件的硬件 ID：这些 ID 针对自己的系统。

## <a name="other-policies"></a>其他策略
* [已定义的扩展 INF 目标评估规则](./extension-inf-targeting-rules.md)
* [驱动程序发布频率](./driver-release-cadence.md)