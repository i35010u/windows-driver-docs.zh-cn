---
title: 安装 COM 端口的高级属性页
description: 安装 COM 端口的高级属性页
keywords:
- 高级 COM 端口属性页 WDK 串行设备
- COM 端口 WDK 串行设备
- COM 端口的默认用户对话框
- "\"覆盖默认值\" 对话框 WDK 串行设备"
- 端口号 WDK 串行设备
- FIFO 控件参数 WDK 串行设备
- COM 端口号 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eaaee5ce64a8fde2471fc0837a1b390f131f09c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812027"
---
# <a name="installing-an-advanced-properties-page-for-a-com-port"></a>安装 COM 端口的高级属性页

"高级" 属性页显示用于设置 FIFO 控件参数和选择 COM 端口号的 "默认用户" 对话框。 但是，您可以通过提供自定义对话框来覆盖默认对话框。

若要为 COM 端口安装系统提供的属性页和默认对话框，请执行以下操作：

1. 实现 Microsoft Win32 属性页提供程序。 有关安装属性表对话框的一般信息，请参阅 [提供设备属性页](../install/overview-of-device-property-pages.md)。

    在属性页提供程序中，调用系统提供的 [**SerialDisplayAdvancedSettings**](/windows/win32/api/msports/nf-msports-serialdisplayadvancedsettings) 例程，该例程显示系统提供的默认对话框。

2. 通过在设备的 [**DDInstall 部分**](../install/inf-ddinstall-section.md)引用的 "*外接程序*" 部分中设置 **EnumPropPages32** 值项，安装属性页提供程序。 请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)中的 **EnumPropPages32** 值项的说明。

若要重写 **SerialDisplayAdvancedSettings** 显示的默认对话框，请执行以下操作：

1. 实现自定义对话 *DLL*。 对话框的入口点是 [**PPORT 的 \_ 高级 \_ 对话框**](/previous-versions/windows/hardware/drivers/ff546956(v=vs.85))类型化例程。

2. 通过在设备的 [**DDInstall 部分**](../install/inf-ddinstall-section.md)引用的 "*外接程序*" 部分中设置 **EnumAdvancedDialog** 项值，安装自定义对话框 DLL。 值项的类型和格式与用于 **EnumPropPages32** 值项的类型和格式相同。
