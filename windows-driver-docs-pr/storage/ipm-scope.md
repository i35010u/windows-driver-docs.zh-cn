---
title: 空闲电源管理范围
description: 空闲电源管理范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c905bc09afaf62826cea59667f0f36437e0d3a63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811682"
---
# <a name="idle-power-management-scope"></a>空闲电源管理范围

Storport Idle 电源管理 (IPM) 为 LUN 而不是适配器提供空闲电源管理。 Storport IPM 不会尝试将适配器置于低功耗状态，前提是其所有 Lun 都处于低功耗状态。 微型端口驱动程序负责管理适配器功能。

仅在以下系统配置中支持 Storport IPM：

- 使用带有单个 SATA 磁盘驱动器的 SATA 适配器的系统

在以下系统配置中不支持 Storport IPM：

- 具有非直接连接存储 (FC、iSCSI 等的系统) 

- 具有外部存储阵列和 RAID 控制器的系统

- 具有 MPIO 的系统

- 具有非 SATA 主机总线适配器的系统

- 将多个磁盘附加到 SATA 适配器的系统
