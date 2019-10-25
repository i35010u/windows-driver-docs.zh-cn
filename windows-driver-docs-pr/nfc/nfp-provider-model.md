---
title: NFP 提供程序模型
description: 近字段邻近性（NFP）提供程序驱动程序模型为 Windows 提供了一个使用 NFP 功能并启用 NFP 方案和用例的通用表面。
ms.assetid: AD8DC80F-5CE2-4547-B951-A82A280F18ED
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5b0bea2e15b8d60a65c506d9c5e88fa3cb72a9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845268"
---
# <a name="nfp-provider-model"></a>NFP 提供程序模型


近字段邻近性（NFP）提供程序驱动程序模型为 Windows 提供了一个使用 NFP 功能并启用 NFP 方案和用例的通用表面。

若要将这些功能公开给 Windows，兼容设备的实施者必须提供实现**GUID\_DEVINTERFACE\_NFP**设备接口的设备驱动程序。 此驱动程序适用于在软件和/或设备硬件上实现的底层 NFP 技术，以形成 NFP 提供程序。

**GUID\_DEVINTERFACE\_NFP**设备接口允许 Windows 使用各种 NFP 技术。 此设备接口的实施者公开的最常见功能是通用的，不特定于任何底层的 NFP 技术。 对此常见功能进行编程以与其他 Windows 应用进行通信时，应能够使用任何 NFP 提供程序，而无需修改应用程序代码。 由于 NFC 是 NFP 空间中的一个前导标准，因此设备接口通过使 NFP 提供程序能够处理本机 NDEF 数据包来支持特定 NFC 行为。 应用可能会依赖于此 NFC 特定功能并仅将其自己的功能限制为启用了 NFC 的 NFP 提供程序。

具有不兼容的 NFP 提供程序的两台电脑无法通过其 NFP 提供程序进行通信。 此规范提供的指导原则足以支持两个经过认证的 Windows 系统的互操作性，因为至少支持一个启用了 NFC 的访问接口。

NFP 提供程序使用发布/订阅模型（其传输由底层 NFP 技术的近程事件触发）来预暂存通信。 消息根据消息类型发布和订阅。 当两个设备根据 NFP 技术近程时，将触发邻近状态，并且所有当前发布的消息将传输到另一台设备上的当前订阅服务器。 此机制提供了一个模型，其中用户在其设备上设置了某些上下文，然后将其与另一台设备点击，以轻松完成此方案。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

