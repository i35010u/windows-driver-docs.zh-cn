---
title: 通过可移动设备功能生成的容器 ID
description: 通过可移动设备功能生成的容器 ID
ms.assetid: e09b1ee5-9ccd-428a-8af3-79f138eb07f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d772fd196b76770b950e42b654348709da02ec3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365468"
---
# <a name="container-ids-generated-from-the-removable-device-capability"></a>通过可移动设备功能生成的容器 ID


从 Windows 7 开始，如果总线驱动程序不能为设备节点提供容器 ID (*devnode*)，它枚举，插即用 (PnP) 管理器使用可移动设备功能来生成所有 devnodes 的容器 ID为物理设备枚举。 总线驱动程序报告的可移动设备功能，以响应[ **IRP_MN_QUERY_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求。

本部分包含以下主题：

[可移动设备功能的概述](overview-of-the-removable-device-capability.md)

[如何从可移动设备功能生成容器 Id](how-container-ids-are-generated-from-the-removable-device-capability.md)

 

 





