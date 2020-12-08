---
title: 处理唤醒事件
description: 处理唤醒事件
keywords:
- 唤醒功能，WDK 网络，处理唤醒事件
- 特定于总线的唤醒线路 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcef588382784dcb919474d54352e1e41809f567
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821373"
---
# <a name="handling-wake-up-events"></a>处理唤醒事件





微型端口驱动程序无法处理 NIC 检测到的唤醒事件。 当 NIC 检测到已启用的唤醒事件时，它将断言特定于总线的唤醒线路。 然后，电源管理器会将一个 power IRP 发送到 NDIS，后者会将微型端口驱动程序发送给一个 [oid \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) oid，请求微型端口驱动程序将 NIC 置于最高性能的 (D0) 状态。

 

