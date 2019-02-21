---
title: 避免设备容器冲突
description: 避免设备容器冲突
ms.assetid: 1c752333-8776-4c5e-bc2f-47ffde60c931
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7de14da7c4ff993b4925377b9ea924b18047182
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533972"
---
# <a name="avoiding-device-container-conflicts"></a>避免设备容器冲突


将两个或多个设备附加到的计算机共享相同的容器 ID (通过使用 Microsoft 操作系统 (OS) 显式定义**ContainerID**描述符或同一个 USB 序列号) 会导致设备容器冲突。 操作系统将解释源自单个设备的设备函数，并将创建单个设备容器。 与设备和 Windows 中，这可能导致意外的行为。

若要避免此问题，请确保 Microsoft OS **ContainerID**描述符值和 USB 序列号是唯一的在单个物理设备。 不共享这些产品系列中的设备之间的值。

如果您的 USB 设备依赖于操作系统以生成基于 USB 的序列号的容器 ID，容器 ID 生成，如下所示：

1.  操作系统将 USB 设备序列号、 供应商 ID、 产品 ID 和修订号生成一个字符串连接在一起。

2.  生成的字符串进行哈希处理成一个 GUID 使用特定于 USB 的命名空间下的 UUID 版本 5 (sha-1) 哈希算法。 生成的容器 ID 是唯一的提供每个设备上的独立硬件供应商 (IHV) 提供唯一的序列号。

 

 





