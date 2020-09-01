---
title: 处理唤醒事件
description: 处理唤醒事件
ms.assetid: 4989d5a4-158c-41db-ab2d-fc995b67a822
keywords:
- 唤醒功能，WDK 网络，处理唤醒事件
- 特定于总线的唤醒线路 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2686018280d148ad1bfa31cd8cce8ff81c693344
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207935"
---
# <a name="handling-wake-up-events"></a>处理唤醒事件





微型端口驱动程序无法处理 NIC 检测到的唤醒事件。 当 NIC 检测到已启用的唤醒事件时，它将断言特定于总线的唤醒线路。 然后，电源管理器会将一个 power IRP 发送到 NDIS，后者会将微型端口驱动程序发送给一个 [oid \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) oid，请求微型端口驱动程序将 NIC 置于最高性能的 (D0) 状态。

 

