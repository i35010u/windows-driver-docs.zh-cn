---
title: 安装 COM 端口的高级属性页
description: 安装 COM 端口的高级属性页
ms.assetid: 056fd245-a9d2-4a10-9e92-fe75e51f6770
keywords:
- 高级的 COM 端口属性页上的 WDK 串行设备
- COM 端口 WDK 串行设备
- 默认 COM 端口的用户对话框
- 重写默认对话框框 WDK 串行设备
- 端口号 WDK 串行设备
- FIFO 控制参数 WDK 串行设备
- COM 端口号 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a26655d71d992b48c5d10c9bfb43d7a47b5ca147
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378605"
---
# <a name="installing-an-advanced-properties-page-for-a-com-port"></a>安装 COM 端口的高级属性页

高级的属性页显示用于设置先进先出控制参数和选择 COM 端口号默认用户对话框。 但是，您可以通过提供一个自定义对话框覆盖默认对话框。

若要安装的 COM 端口的系统提供的属性页和默认对话框中，执行以下操作：

1. 实现 Microsoft Win32 属性页提供程序。 有关安装属性表对话框的详细信息，请参阅[提供的设备属性页](https://docs.microsoft.com/windows-hardware/drivers/install/providing-device-property-pages)。

    在属性页提供程序中调用的系统提供[ **SerialDisplayAdvancedSettings** ](https://docs.microsoft.com/windows/desktop/api/msports/nf-msports-serialdisplayadvancedsettings)例程，后者将显示系统提供的默认值对话框。

2. 安装属性页提供程序设置**EnumPropPages32**值中的条目*添加注册表部分*通过设备的引用[ **DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section). 请参阅的说明**EnumPropPages32**值中的条目[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

若要重写默认显示的对话框**SerialDisplayAdvancedSettings**，执行以下操作：

1. 实现自定义对话框*DLL*。 对话框中的入口点是[ **PPORT\_高级\_对话框**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546956(v=vs.85))-类型化例程。

2. 通过设置安装自定义对话框 DLL **EnumAdvancedDialog**中的项值*添加注册表部分*引用某一设备[ **DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section). 类型和值项的格式是用于相同**EnumPropPages32**值项目。
