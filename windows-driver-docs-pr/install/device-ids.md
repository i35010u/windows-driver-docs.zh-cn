---
title: 设备 ID
description: 设备 ID 是一个字符串，报告的设备的枚举器。 设备具有只有一个设备 id。 设备 ID 具有相同的格式为硬件 id。
ms.assetid: a71b64bc-319e-4133-810b-7fd417cf0af8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565b64f9f27540cf0468b98847bc44300d4b8c00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387134"
---
# <a name="device-id"></a>设备 ID


设备 ID 是一个字符串，由设备的报告*枚举器*。 设备具有只有一个设备 id。 设备 ID 已与相同的格式[硬件 ID](hardware-ids.md)。




插即用 (PnP) 管理器使用设备 ID 来为设备的枚举器创建一个用于设备注册表项下的子项。

若要获取设备 ID，请使用[ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)请求并设置**Parameters.QueryId.IdType**字段**BusQueryDeviceID**。

 

 





