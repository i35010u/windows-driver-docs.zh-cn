---
title: PF 微型端口驱动程序的初始化序列
description: PF 微型端口驱动程序的初始化序列
ms.assetid: A8891D72-314D-4648-ABCA-E917C3091FF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31b29dd4740a80835f7b45c4ae8abdaab29259e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546743"
---
# <a name="initialization-sequence-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的初始化序列


本部分介绍有关 PCI Express (PCIe) 物理函数 (PF) 的要求和准则的微型端口驱动程序初始化序列。 PF 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的组件。

本部分包括以下主题：

[DriverEntry PF 微型端口驱动程序的指导原则](driverentry-guidelines-for-pf-miniport-drivers.md)

[*MiniportAddDevice* PF 微型端口驱动程序的准则](miniportadddevice-guidelines-for-pf-miniport-drivers.md)

[*MiniportInitializeEx* PF 微型端口驱动程序的准则](miniportinitializeex-guidelines-for-pf-miniport-drivers.md)

**请注意**  初始化为 PCIe 虚拟函数 (VF) 的 SR-IOV 网络适配器上的微型端口驱动程序的信息，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

 

 





