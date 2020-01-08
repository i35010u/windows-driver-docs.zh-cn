---
title: Storport 空闲电源管理概述
description: Storport 空闲电源管理概述
ms.assetid: 1ad47775-4d7a-47c4-83eb-774e58c863d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 100d38c7aa33ee41cb292b819ee1eb645eadb4f5
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606377"
---
# <a name="storport-idle-power-management-overview"></a>Storport 空闲电源管理概述

Storport 空闲电源管理（IPM）允许 classpnp 和 disk 类驱动程序在某个时间段处于空闲状态时将 SCSI 停止单元命令发送到该设备。 空闲时间可由系统管理员进行配置。 Storport 微型端口驱动程序负责使用该命令来节省 Storport 微型端口驱动程序的能力。 以下部分更详细地介绍了 IPM。

- [Scope](ipm-scope.md)

- [假设](ipm-assumptions.md)

- [配置和用法](ipm-configuration-and-usage.md)

- [硬盘驱动器空闲超时](ipm-hard-disk-drive-idle-timeout.md)
