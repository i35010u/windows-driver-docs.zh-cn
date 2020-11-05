---
title: “游戏杆支持”概述
description: “游戏杆支持”概述
ms.assetid: 09fcbdf0-4e70-4144-9afc-4b085a2b4ba7
keywords:
- 游戏杆 WDK HID
- 操纵杆 WDK HID，关于操纵杆
- 微型驱动程序 WDK 操纵杆
- 虚拟游戏杆驱动程序 WDK HID
- VJoyD WDK HID
- 虚拟游戏杆驱动程序 WDK HID，关于 VJoyD
- VJoyD WDK HID，关于 VJoyD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92c182c4110ef8875aefff7ec816c963a462776
ms.sourcegitcommit: 3464f10ffa0727e38fbe225cfab52bb8c2bb1747
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93352970"
---
# <a name="joystick-support-overview"></a>“游戏杆支持”概述





Microsoft DirectX 提供的游戏杆支持类型与版本之间存在差异。 在 Windows 95/98/Me 中，DirectX 支持以下两种方法来自定义游戏杆功能：通过 Windows 注册表中的自定义项和通过虚拟设备驱动程序 (VxD) 创建，这称为 *操纵杆微型驱动程序* 。 DirectX 版本1.0、2.0 和3.0 中使用的微型驱动程序支持原始的微型驱动程序接口，在 DirectX 3.0 接口中有细微差别。 除了原始微型驱动程序模型之外，DirectX 版本5.0 及更高版本还包括一个通常单独描述的备用驱动程序接口。

Windows 95/98/Me 游戏杆驱动程序和配置程序支持插入 IBM 标准游戏端口的模拟操纵杆。 游戏杆制造商可以使操纵杆配置程序可自定义，并向最终用户提供有关如何自定义游戏杆的明确指导。 游戏杆可以通过注册表向 Windows 95/98/Me 发送相关功能。 这些功能包括使用限制、视图点 (POV) 头衔、rudders 以及游戏杆按钮的数目。

所有非 IBM 标准游戏杆，如 "游戏杆" 加速器驱动的 "游戏操纵杆" 和 "模拟游戏操纵杆" 除了自定义注册表信息外，还必须提供操纵杆微型驱动程序。 游戏杆 OEM 可以编写微型驱动程序，它提供对非标准操纵杆硬件的访问。 这为数字操纵杆提供了一种机制，使数字操纵杆能与使用操纵杆应用程序编程接口 (API) 的任何基于 Windows 的游戏一起工作。

驱动程序模型最多可以处理六个轴、一个 POV hat 和一个双字的按钮，使 OEM 可以轻松地为新硬件创建微型驱动程序，而不是使用当前游戏端口所允许的更高的自由度。 操纵杆微型驱动程序可为硬件供应商提供完全的灵活性，并使游戏创建者能够将安装的基础与标题结合使用。 在 DirectX 5.0 和更高版本中，模拟游戏杆支持还被分隔到使用新接口的微型驱动程序。 仅当配置了模拟游戏端口时，才会加载此新接口。 轮询是使用三个额外的 POV 头衔来扩展的，另外还有三个包含按钮数据的双引号，另外还提供了一个方法，用于指定它返回每个轴的速度、加速度和/或强制数据。

当前的虚拟游戏杆驱动程序 (VJoyD) 允许配置最多16个设备，可由微型驱动程序驱动的任意数量的设备。 微型驱动程序到设备的配置可以是一对一或一对多。

本节包括：

[原始接口](original-interface.md)

[DirectX 5.0 接口](directx-5-0-interface.md)

[INF 文件创建](creating-an-inf-file.md)

[注册表设置](registry-settings2.md)

[VJoyD 微型驱动程序重写](vjoyd-minidriver-override.md)

[轴选择](axis-selection.md)

 

