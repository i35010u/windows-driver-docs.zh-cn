---
title: 处理可移动子设备
description: 处理可移动子设备
ms.assetid: 0edc0331-7178-4986-b818-9f1ee8f12995
keywords:
- 显示可移动子设备 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f0a3a58964bfb1cca7aaed2aa4fb1d385073845
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524447"
---
# <a name="handling-removable-child-devices"></a>处理可移动子设备


可移动子设备更改与另一种设备，因此驱动程序可以防止插 (PnP) 使用的数据的原始子设备时，应检测到的微型端口驱动程序。 例如，在用户切换监视器时，应检测到的微型端口驱动程序。

如果扩展显示信息的数据 (EDID) 为附加的监视器更改为视频的微型端口驱动程序的连续调用之间[ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)函数，而不是撕裂现象关闭原始的监视器堆栈和新监视器生成一个新的堆栈，视频端口驱动程序将修改当前堆栈的状态。 虽然图形子系统可以确定新监视器的功能，因为原始堆栈已不在拆解，其他操作系统组件 (如，PnP) 使用原始的监视器的功能数据。

微型端口驱动程序可以检测到附加的监视器的更改并执行下列操作来防止从使用原始的监视器的数据即插即用之一：

1.  微型端口驱动程序可以报告显示器都不是为了向下强制拆解，前者监视器堆栈的存在。 然后，若要强制重新枚举子设备以报告新监视器的视频端口驱动程序，该视频的微型端口驱动程序调用[ **VideoPortEnumerateChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff570297)函数。 微型端口驱动程序应调用**VideoPortEnumerateChildren**计划重新枚举子设备的第一个枚举，用于报告，监视器已断开连接后，才完成。

2.  响应的微型端口驱动程序可以在相应的计算机和监视器配置 （请参阅以下异常），其*HwVidGetVideoChildDescriptor*变量中的新监视器的*UId*参数指向。 此值必须不同于以前的监视器的微型端口驱动程序使用的值。

适用于高级配置和电源接口 (ACPI) 枚举监视器，第一种机制是通常更可取，因为 32 位设备 Id 与 BIOS 实现。 因此，指定不同的 32 位设备 ID 不可以。

 

 





