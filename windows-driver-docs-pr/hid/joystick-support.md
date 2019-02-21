---
title: 游戏杆支持
description: 游戏杆支持
ms.assetid: 09fcbdf0-4e70-4144-9afc-4b085a2b4ba7
keywords:
- 游戏杆 WDK HID
- 游戏杆 WDK HID，有关游戏杆
- 微型驱动程序 WDK 游戏杆
- 虚拟游戏杆驱动程序 WDK HID
- VJoyD WDK HID
- 有关 VJoyD WDK HID 虚拟游戏杆驱动程序
- VJoyD WDK HID，有关 VJoyD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66ecf1c1d9a58ff6cde5ea4d60d2ade175e4dee8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545358"
---
# <a name="joystick-support"></a>游戏杆支持





有差异从一个版本到另一个版本中提供了 Microsoft DirectX 的游戏杆支持的类型。 在 Windows 95/98/我，DirectX 支持用于自定义游戏杆功能两种方法： 通过 Windows 注册表中的自定义项和虚拟设备驱动程序 (VxD) 创建，这作为调用*游戏杆微型驱动程序*。 DirectX 版本 1.0、 2.0 和 3.0 中使用微型驱动程序支持的原始的微型驱动程序接口，在 DirectX 3.0 接口有细微差别。 除了原始的微型驱动程序模型中，DirectX 版本 5.0 及更高版本，包括单独通常描述的可选驱动程序接口。

Windows 95/98/我游戏杆驱动程序和配置程序支持插入到 IBM 标准游戏端口的模拟游戏杆。 游戏杆制造商可以使游戏杆配置程序可自定义，并向最终用户如何自定义游戏杆提供显式说明。 游戏杆，Windows 95/98/我可以发出及其相关功能通过注册表。 这些功能可以包括使用限制、 的角度 (POV) 尖角符号、 舵和游戏杆按钮的数目。

所有非 IBM 标准游戏杆，如数字游戏杆、 MIDI 游戏杆和模拟游戏杆驱动的游戏杆加速器必须提供自定义注册表信息的补充游戏杆微型驱动程序。 游戏杆 OEM 可以编写能够使用非标准游戏杆硬件的微型驱动程序。 这提供了一种数字游戏杆以使用任何基于 Windows 的游戏，使用游戏杆应用程序编程接口 (API) 的机制。

驱动程序模型可以处理最多六个轴、 POV hat 和双字的按钮，以便可以轻松地创建 OEM 允许使用微型驱动程序的使用比当前游戏端口的更高自由度的新硬件。 游戏杆微型驱动程序与硬件供应商提供完全的灵活性，并允许游戏创建者可以使用自己的书名使用安装的基数。 在 DirectX 5.0 及更高版本，模拟游戏杆支持还被分成微型驱动程序使用新接口。 仅当配置一个模拟游戏端口时加载此新接口。 轮询扩展具有三个额外 POV 帽，三个包含按钮数据和方法来指定它返回的速度，加速和/或强制数据的每个轴的详细双字。

当前虚拟游戏杆驱动程序 (VJoyD) 允许的最多 16 个设备，微型驱动程序可由任意数量的配置。 微型驱动程序到设备的配置可以是一对一或一对多。

本部分包括：

[Joystick Driver Model](joystick-driver-model.md)

[微型驱动程序提供的回调](minidriver-supplied-callbacks.md)

[原始接口](original-interface.md)

[DirectX 5.0 接口](directx-5-0-interface.md)

[INF 文件创建](creating-an-inf-file.md)

[注册表设置](registry-settings2.md)

[VJoyD Minidriver Override](vjoyd-minidriver-override.md)

[轴选择](axis-selection.md)

 

 




