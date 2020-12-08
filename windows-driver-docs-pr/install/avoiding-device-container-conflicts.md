---
title: 避免设备容器冲突
description: 避免设备容器冲突
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1d2a6f78ecf6895631315012962c7e12bd9312
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783193"
---
# <a name="avoiding-device-container-conflicts"></a>避免设备容器冲突


如果将两个或更多设备连接到共享相同容器 ID (通过使用 Microsoft 操作系统 (OS) **ContainerID** 描述符或相同 USB 序列号显式定义的计算机，) 将导致设备容器发生冲突。 操作系统会将设备功能解释为源自单个设备，并将创建单个设备容器。 这可能会导致设备和 Windows 中出现意外的行为。

若要避免此问题，请确保 Microsoft 操作系统 **ContainerID** 描述符值和 USB 序列号对于单个物理设备是唯一的。 请勿在产品系列中的设备之间共享这些值。

如果 USB 设备依赖于操作系统基于 USB 序列号生成容器 ID，则会生成容器 ID，如下所示：

1.  操作系统会连接 USB 设备序列号、供应商 ID、产品 ID 和修订号，以生成字符串。

2.  通过在特定于 USB 的命名空间下使用 UUID 版本 5 (SHA-1) 哈希算法，可将结果哈希转换为 GUID。 如果独立硬件供应商 (IHV) 在每台设备上提供唯一序列号，则生成的容器 ID 将是唯一的。

 

 





