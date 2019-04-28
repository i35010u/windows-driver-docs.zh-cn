---
Description: 介绍通用串行总线 (USB) 2.0 选择性挂起机制的限制。
title: USB 2.0 机制的限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d345cd6b3b5da73208f70d6e9b3f5396a0299e9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355467"
---
# <a name="limitations-of-usb-20-mechanism"></a>USB 2.0 机制的限制


介绍通用串行总线 (USB) 2.0 选择性挂起机制的限制。 然后，它提供 USB 3.0 链接电源管理 (LPM) 功能和如何它可以在一起的选择性挂起机制以减少系统功耗的概述。 最后，它列出了在 LPM USB 控制器、 中心和设备中实现常见的缺陷。

USB 2.0 规范定义了一种节省电源，允许设备 （或中心） 进入挂起的状态时不使用的机制。 此机制称为[选择性挂起](https://go.microsoft.com/fwlink/p/?linkid=230962)。 选择性挂起是强大的机制，以节约能源但退出延迟在数十毫秒。 选择性挂起需要软件以取消所有传输到设备，然后显式将设备发送到挂起状态。 因此，此机制是实用，仅当设备处于空闲状态较长的时间，通常以秒为单位。

选择性挂起还强加了严格的电源消耗限制设备处于挂起状态。 这些限制可能是明显少于处于工作状态时在设备施加的限制。 如果设备不能保留所需的唤醒功能，并将自身限制为的限制，则它不能发送到选择性挂起。

例如，在某些目前的限制，鼠标可能无法从选择性挂起时唤醒用户移动鼠标，因为没有足够的电力来光传感器。 同一鼠标可能能够唤醒由于按下按钮。 此类鼠标无法发送到选择性挂起，而不会影响用户体验。

 

 




