---
title: 设备 ID
description: 设备 ID 是设备的枚举器报告的字符串。 设备只有一个设备 ID。 设备 ID 与硬件 ID 的格式相同。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7b0d1037b98958e43686146c53eee277b9274ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827733"
---
# <a name="device-id"></a>设备 ID


设备 ID 是设备的 *枚举器* 报告的字符串。 设备只有一个设备 ID。 设备 ID 与 [硬件 id](hardware-ids.md)的格式相同。




即插即用 (PnP) 管理器使用设备 ID 在设备枚举器的注册表项下为设备创建子项。

若要获取设备 ID，请使用 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md) 请求，并将 **IdType** 字段设置为 **BusQueryDeviceID**。

 

