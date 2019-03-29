---
title: 通过可移动设备功能生成的容器 ID
description: 通过可移动设备功能生成的容器 ID
ms.assetid: e09b1ee5-9ccd-428a-8af3-79f138eb07f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c095c8c503a36b56e3d01ee25b8984e0388d5f63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565300"
---
# <a name="container-ids-generated-from-the-removable-device-capability"></a>通过可移动设备功能生成的容器 ID


从 Windows 7 开始，如果总线驱动程序不能为设备节点提供容器 ID (*devnode*)，它枚举，插即用 (PnP) 管理器使用可移动设备功能来生成所有 devnodes 的容器 ID为物理设备枚举。 总线驱动程序报告的可移动设备功能，以响应[ **IRP_MN_QUERY_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff551664)请求。

本部分包含以下主题：

[可移动设备功能的概述](overview-of-the-removable-device-capability.md)

[如何从可移动设备功能生成容器 Id](how-container-ids-are-generated-from-the-removable-device-capability.md)

 

 





