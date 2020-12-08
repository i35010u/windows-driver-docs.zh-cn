---
title: PF 微型端口驱动程序的初始化序列
description: PF 微型端口驱动程序的初始化序列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc993a9a50a795e569c758eb40c094e5057259ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841177"
---
# <a name="initialization-sequence-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的初始化序列


本部分介绍 PCI Express (PCIe 的小型端口驱动程序初始化序列的要求和指导原则) 物理功能 (PF) 。 PF 是网络适配器的一个组件，它支持 (SR-IOV) 的单个根 i/o 虚拟化。

本节包括下列主题：

[PF 微型端口驱动程序的 DriverEntry 指导原则](driverentry-guidelines-for-pf-miniport-drivers.md)

[*MiniportAddDevice* PF 微型端口驱动程序的准则](miniportadddevice-guidelines-for-pf-miniport-drivers.md)

[*MiniportInitializeEx* PF 微型端口驱动程序的准则](miniportinitializeex-guidelines-for-pf-miniport-drivers.md)

**注意**  有关在 SR-IOV 网络适配器上初始化 PCIe 虚拟功能 (VF) 的微型端口驱动程序的信息，请参阅 [初始化 Vf 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

 

 





