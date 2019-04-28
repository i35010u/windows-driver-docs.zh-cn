---
title: 支持显示输出和 ACPI 事件
description: 系统配置和设备电源控制的综合方法内置于 Windows，基于 ACPI 规范。
ms.assetid: CD5BC59A-4C15-4111-BF4F-13DC04F6874F
keywords:
- ACPI 显示 WDK 显示
- 基于 ACPI 显示热键 WDK 显示
- 显示热键 WDK 显示
- BIOS 显示 WDK 显示的控件
- 自动显示切换 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a1bf1a049a3685b00da1bf134c191d24a76cc44
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331279"
---
# <a name="supporting-display-output-and-acpi-events"></a>支持显示输出和 ACPI 事件


系统配置和设备电源控制的综合方法内置于 Windows，基于高级配置和电源接口 (ACPI) 规范。 Windows 支持驱动程序可用于管理的配置和显示输出设备的电源的功能。 有关详细信息，请参阅 》 上 ACPI 规范[ACPI 网站](https://go.microsoft.com/fwlink/p/?linkid=57185)。

## <a name="span-idbiosrequirementstosupportdisplayoutputdevicesspanspan-idbiosrequirementstosupportdisplayoutputdevicesspanspan-idbiosrequirementstosupportdisplayoutputdevicesspanbios-requirements-to-support-display-output-devices"></a><span id="BIOS_Requirements_to_Support_Display_Output_Devices"></span><span id="bios_requirements_to_support_display_output_devices"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_DISPLAY_OUTPUT_DEVICES"></span>支持的输出显示设备的 BIOS 要求


显示微型端口驱动程序或由系统 BIOS 支持显示输出设备配置的 ACPI 方法中。 [ **DxgkDdiNotifyAcpiEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff559695)函数调用以通知有关 ACPI 事件显示微型端口驱动程序。 例如，当用户按下键盘快捷方式为输出设备开关， **DxgkDdiNotifyAcpiEvent** ACPI 与调用函数\_通知\_周期\_显示\_热键通知和请求类型的 DXGK\_ACPI\_更改\_显示\_模式。 因此，操作系统将调用[ **DxgkDdiRecommendFunctionalVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559775)函数查询选择的显示输出设备。

Dispmprt.h 中定义的 ACPI 显示输出的下列别名：

-   ACPI\_方法\_显示\_DOD-枚举附加到显示适配器的所有设备。 如果集成的控制器支持转换的输出设备，则需要使用此方法。 这是美国国防部的别名名称\_ACPI 规范所定义的方法。
-   ACPI\_方法\_显示\_DOS 的指示系统固件能否自动切换活动显示输出。 这是 SOD 的别名名称\_ACPI 规范所定义的方法。 允许的参数如下：
    -   ACPI\_ARG\_启用\_交换机\_事件。 系统固件应自动切换活动的状态显示输出设备。 相反，它必须在与每个显示输出设备相关联的状态变量中保存所需的更改并生成显示切换事件。 操作系统可以查询设备的活动状态，通过调用 ACPI\_方法\_输出\_DG 方法。
    -   ACPI\_ARG\_启用\_自动\_开关。 系统固件应会自动切换活动的状态显示输出设备，而不与操作系统进行交互。 它不生成显示切换事件。
    -   ACPI\_ARG\_禁用\_交换机\_事件。 状态系统固件不应执行任何操作;也就是说，不切换输出设备或通知操作系统。 ACPI 返回的值\_方法\_输出\_DG 方法被锁定。
-   ACPI\_方法\_输出\_DC-返回显示的状态输出设备。 这是 CSD 的别名名称\_ACPI 规范所定义的方法。
-   ACPI\_方法\_输出\_DG-检查是否显示的状态输出设备处于活动状态。 这是 SGD 的别名名称\_ACPI 规范所定义的方法。
-   ACPI\_方法\_输出\_DSS-设置显示的状态为活动或非活动的输出设备。 这是固态硬盘的别名名称\_ACPI 规范所定义的方法。 操作系统管理此操作以避免闪烁。
-   ACPI\_方法\_显示\_GPD-查询 CMOS 条目，以确定哪些视频设备发布在启动时。 这是 DPG 的别名名称\_ACPI 规范所定义的方法。
-   ACPI\_方法\_显示\_SPD-确定哪个视频设备发布在启动时的 CMOS 项更新。 这是分发点的别名名称\_ACPI 规范所定义的方法。
-   ACPI\_方法\_显示\_VPO-确定哪些视频选项的实现。 这是 OPV 的别名名称\_ACPI 规范所定义的方法。

## <a name="span-idexternalasynchronouseventsspanspan-idexternalasynchronouseventsspanspan-idexternalasynchronouseventsspanexternal-asynchronous-events"></a><span id="External_Asynchronous_Events"></span><span id="external_asynchronous_events"></span><span id="EXTERNAL_ASYNCHRONOUS_EVENTS"></span>外部异步事件


有关影响显示输出设备的外部，异步事件，必须通知给操作系统。 Dispmprt.h 中定义和使用中的以下通知和相关的请求类型[ **DxgkDdiNotifyAcpiEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff559695)函数。

-   ACPI\_通知\_周期\_显示\_热键-通知操作系统用户已按周期显示键盘快捷方式。
-   ACPI\_通知\_下一步\_显示\_热键-通知操作系统用户已按下一步显示键盘快捷方式。
-   ACPI\_通知\_PREV\_显示\_热键-通知操作系统用户已按前面显示键盘快捷方式。

**请注意**之前通知依赖于由用户按下键盘快捷方式时引起的事件的处理。

 

以下是显示微型端口驱动程序可以对操作系统进行的请求的类型。

-   DXGK\_ACPI\_更改\_显示\_模式-请求启动模式更改为新建议的活动的视频存在网络 (VidPN)。
-   DXGK\_ACPI\_轮询\_显示\_子级的请求轮询的子级显示适配器的连接。

**请注意**以前的请求是的值*AcpiFlags*返回参数[ **DxgkDdiNotifyAcpiEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff559695)函数。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[支持在集成的显示器的亮度控件](supporting-brightness-controls-on-integrated-display-panels.md)

 

 






