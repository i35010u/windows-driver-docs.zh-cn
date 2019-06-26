---
title: 为多功能设备创建资源映射
description: 为多功能设备创建资源映射
ms.assetid: 332eef11-4056-4fe0-87ed-4305c091bab1
keywords:
- WDK 的多功能设备，资源映射
- 资源映射 WDK 多功能设备
- 子函数资源映射 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1392401397dbd09a0df1ece29fedf8e778898fd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362928"
---
# <a name="creating-resource-maps-for-a-multifunction-device"></a>为多功能设备创建资源映射





一个*资源映射*标识使用的子函数的多功能设备的资源。 使用指定资源映射[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。 如果多功能设备需要资源映射，则设备 INF 通常包含设备的每个函数的资源映射。

有两种类型的资源映射 −*标准*资源映射并*不同*资源映射。 本部分介绍如何构造资源映射，并且包括以下主题：

[创建标准版资源映射](creating-standard-resource-maps.md)

[创建不同的资源映射](creating-varying-resource-maps.md)

可以使用只有标准版资源映射描述某些多功能设备。 其他人需要不同的资源映射或映射的标准和不同的组合。 仍另一些根本要求任何资源映射。 请参阅[支持多功能 PC 卡设备](supporting-multifunction-pc-card-devices.md)来确定哪些多功能设备需要资源映射。

 

 




