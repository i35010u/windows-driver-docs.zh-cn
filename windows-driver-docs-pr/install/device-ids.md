---
title: 设备 ID
description: 设备 ID 是一个字符串，报告的设备的枚举器。 设备具有只有一个设备 id。 设备 ID 具有相同的格式为硬件 id。
ms.assetid: a71b64bc-319e-4133-810b-7fd417cf0af8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2ee9b58bd89fba27d4f14933d6ffe2a8a19d447
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548195"
---
# <a name="device-id"></a>设备 ID


设备 ID 是一个字符串，由设备的报告*枚举器*。 设备具有只有一个设备 id。 设备 ID 已与相同的格式[硬件 ID](hardware-ids.md)。




插即用 (PnP) 管理器使用设备 ID 来为设备的枚举器创建一个用于设备注册表项下的子项。

若要获取设备 ID，请使用[ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)请求并设置**Parameters.QueryId.IdType**字段**BusQueryDeviceID**。

 

 





