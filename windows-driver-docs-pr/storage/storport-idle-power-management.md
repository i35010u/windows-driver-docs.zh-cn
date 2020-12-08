---
title: Storport 空闲电源管理概述
description: Storport 空闲电源管理概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc5972388377046fad36db13c97a3e419b3b5758
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820517"
---
# <a name="storport-idle-power-management-overview"></a>Storport 空闲电源管理概述

Storport Idle 电源管理 (IPM) 使 classpnp 和 disk 类驱动程序可以在某个时间段处于空闲状态时将 SCSI 停止单元命令发送到该设备。 空闲时间可由系统管理员进行配置。 Storport 微型端口驱动程序负责使用该命令来节省 Storport 微型端口驱动程序的能力。 以下部分更详细地介绍了 IPM。

- [范围](ipm-scope.md)

- [假设](ipm-assumptions.md)

- [配置和使用情况](ipm-configuration-and-usage.md)

- [硬盘驱动器空闲超时](ipm-hard-disk-drive-idle-timeout.md)
