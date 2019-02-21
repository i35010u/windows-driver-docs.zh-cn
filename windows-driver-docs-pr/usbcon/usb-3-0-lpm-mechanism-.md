---
Description: This topic describes the USB 3.0 LPM mechanism.There is an addendum to the official USB 2.0 Specification (USB2_LinkPowerMangement_ECN), which defines LPM for newer USB 2.0 hardware.
title: USB 3.0 LPM 机制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2d787b2fec190dd25b1f5a4d8e903963577bc8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520734"
---
# <a name="usb-30-lpm-mechanism"></a>USB 3.0 LPM 机制


本主题介绍的 USB 3.0 LPM 机制。

没有正式的附录[USB 2.0 规范](https://go.microsoft.com/fwlink/p/?linkid=230961)(USB2\_LinkPowerMangement\_ECN)，用于定义 LPM 的较新的 USB 2.0 硬件。 本主题不涉及该 USB 2.0 LPM 机制。 本主题旨在说明 USB 3.0 LPM 状态，尤其是 U1 和 U2。

USB 3.0 设备也支持选择性挂起。 可以克服这些限制的选择性挂起，正式的 USB 3.0 规范定义了更精细的电源管理状态。 在介绍之前这些状态以及如何使用它们来改进电源管理，让我们先了解链接的概念。

## <a name="what-is-a-link"></a>什么是链接


两个 USB 端口之间存在的 USB 连接：

-   下游端口 （DS 端口） 的主机或集线器。
-   上游端口 （美国端口） 的附加的设备或中心。

一个*链接*是一对 DS 和我们端口; 端口称为链接合作伙伴。 每个端口都具有两个层。 物理层传输或接收的字节数或其他控件信号的序列。 逻辑层管理物理层，并确保顺利运行的链接合作伙伴之间的信息。 逻辑层也是责任的任何缓冲可能是所必需的信息流动。

## <a name="u-states"></a>U 状态


根据 USB 2.0 规范中，链接进入低功耗状态 （占用较少的电量比工作状态） 仅当下游设备进入挂起的状态通过选择性挂起机制。 USB 3.0 规范将从设备的电源状态的链接的电源状态中分离出来。 此规范定义 LPM 功能 （请参阅规范中的部分 C.1） 引用的物理和逻辑层的一对构成链接的端口的电源管理。 该规范定义名为 U，正在从状态到 U3 U0 的四个链接的电源状态。 活动链接处于状态 U0。

在剩余空闲一段时间后链接合作伙伴以渐进方式输入 U1 （备用快捷退出），然后 U2 （备用速度较慢的退出）。 足够的时间处于空闲状态后，软件通过将命令发送到 DS 端口链接合作伙伴启动到 U3 的转换。

软件，需将链接发送给 U3，步骤的 USB 2.0 选择性挂起所需的步骤相同。 当链接进入 U3 时，设备必须进入挂起的状态。 因此，设备会受到与使用 USB 2.0 选择性挂起的类似限制。 为了克服这些限制，USB 3.0 规范定义了 U1 和 U2 状态。

## <a name="advantages-of-u1-and-u2"></a>U1 和 U2 的优点


U1 和 U2 状态用于补充选择性挂起，这可能会导致重大节能。 软件配置 U1 或 U2 转换链接合作伙伴后，硬件进入自主操作无需任何软件操作的状态。 从 U1 和 U2 的退出时间 （从几毫秒到微秒为单位） 的速度相当快，并对设备的性能产生的影响更小。 这允许多更好的电源管理其中的链接可进入和退出这些状态，即使设备正在使用中。

例如，与同步终结点设备可以将该链接 U1 或 U2 不同服务间隔期之间。 若要保存一些电量，当设备处于空闲状态时，它可以在甚至选择性挂起获取调用之前向这些状态发送其上游链接。 没有任何限制在该设备可以绘制时的链接有 U1 或 U2 多少电力。 如果链接是 U1 或 U2 中将设备保持正常通电。 因此，与不同的选择性挂起，设备可以发送其链接到 U1 或 U2 而不会丢失任何功能。

 

 




