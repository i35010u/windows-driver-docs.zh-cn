---
title: IPM 作用域
description: IPM 作用域
ms.assetid: fa34f703-ab02-4a0d-96ae-e7cb89756992
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021d0914aedea0a196bf90d558c870ae35dca5b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534360"
---
# <a name="ipm-scope"></a>IPM 作用域


Storport 空闲电源管理 (IPM) 提供了 LUN，而不是适配器的空闲状态的电源管理。 Storport IPM 不会尝试将该适配器放置在低功耗状态，如果所有 Lun 在低功耗状态。 微型端口驱动程序负责管理适配器的电源。

Storport IPM 支持以下系统配置中：

使用 SATA 适配器与连接的单一 SATA 磁盘驱动器的系统

Storport IPM 不支持下列系统配置中：

具有非直接附加的存储 （光纤通道、 iSCSI 和其他人） 的系统

具有外部存储阵列和 RAID 控制器的系统

如果系统包含 MPIO

具有非 SATA 系统主机总线适配器

具有多个磁盘附加到 SATA 适配器的系统

 

 




