---
title: 设备 ID
description: 设备 ID 是设备的枚举器报告的字符串。 设备只有一个设备 ID。 设备 ID 与硬件 ID 的格式相同。
ms.assetid: a71b64bc-319e-4133-810b-7fd417cf0af8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652845ea629753d1f1fbf3ad68f3c098c7722890
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097023"
---
# <a name="device-id"></a>设备 ID


设备 ID 是设备的 *枚举器*报告的字符串。 设备只有一个设备 ID。 设备 ID 与 [硬件 id](hardware-ids.md)的格式相同。




即插即用 (PnP) 管理器使用设备 ID 在设备枚举器的注册表项下为设备创建子项。

若要获取设备 ID，请使用 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md) 请求，并将 **IdType** 字段设置为 **BusQueryDeviceID**。

 

