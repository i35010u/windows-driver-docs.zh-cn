---
title: 已检验版本断点和消息
description: 已检验版本断点和消息
ms.assetid: 99b27487-eb95-4303-bad6-0b7ed8b450f0
keywords:
- 断点 WDK
- 检查内部版本号 WDK，断点
- 检查内部版本号 WDK，消息
- 检查生成邮件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ca20234192e1bf0de15352a2883a548e74e129a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561958"
---
# <a name="checked-build-breakpoints-and-messages"></a>已检验版本断点和消息


## <span id="ddk_checked_build_breakpoints_and_messages_tools"></span><span id="DDK_CHECKED_BUILD_BREAKPOINTS_AND_MESSAGES_TOOLS"></span>


本主题包含列表和说明的一些常见的断点并[ **DbgPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff543632)驱动程序可能会遇到调试内部版本中的消息。

<span id="____DPC_routine___1_sec_---_This_is_not_a_break_in_KeUpdateSystemTime"></span><span id="____dpc_routine___1_sec_---_this_is_not_a_break_in_keupdatesystemtime"></span><span id="____DPC_ROUTINE___1_SEC_---_THIS_IS_NOT_A_BREAK_IN_KEUPDATESYSTEMTIME"></span>**\*\*\* DPC 例程&gt;1 秒---这不是在 KeUpdateSystemTime 中断**  
只需发出断点之前，会出现此消息。 它指示活动的驱动程序所用超过一秒 DPC 的例程中。

<span id="____isr_at_0x_________________nnnnnnnn_________________took_over_.5_second"></span><span id="____ISR_AT_0X_________________NNNNNNNN_________________TOOK_OVER_.5_SECOND"></span>**\*\*\* 在 0xisr** *nnnnnnnn* **花费了超过.5 秒**  
只需发出断点之前，会出现此消息。 它指示中断服务例程的入口点 0x*nnnnnnnn*执行多个 500 毫秒。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________FAILED_TO_INITIALIZE___0XNNNNNNNN"></span>**IOINIT:内置的驱动程序** *xxxxxx* **未能初始化 − 0 x * * * nnnnnnnn*引导启动驱动程序命名为*xxxxxx*返回失败状态0x*nnnnnnnn * 从其**DriverEntry**入口点。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOINIT:内置的驱动程序** *xxxxxx* **花费了** *y.z* **s 初始化**  
在引导启动驱动程序名为*xxxxxx*执行*y.z*秒 （这是时间超过 5 秒的预期最大时间） 在其**DriverEntry**入口点。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOINIT:内置的驱动程序** *xxxxxx* **花费了** *y.z* **s，无法初始化**  
在引导启动驱动程序名为*xxxxxx*执行*y.z*秒 （这是时间超过 5 秒的预期最大时间） 在其**DriverEntry**入口点。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOLOAD:驱动程序** *xxxxxx* **花费了** *y.z* **s 初始化**  
名为的驱动程序*xxxxxx*执行*y.z*秒 （这是时间超过 5 秒的预期最大时间） 在其**DriverEntry**入口点。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOLOAD:驱动程序** *xxxxxx* **花费了** *y.z* **s，无法初始化**  
名为的驱动程序*xxxxxx*执行*y.z*秒 （这是时间超过 5 秒的预期最大时间） 在其**DriverEntry**入口点。

<span id="IopLoadDriver__A_PnP_driver__________________xxxxxx_________________does_not_support_DriverUnload_routine"></span><span id="ioploaddriver__a_pnp_driver__________________xxxxxx_________________does_not_support_driverunload_routine"></span><span id="IOPLOADDRIVER__A_PNP_DRIVER__________________XXXXXX_________________DOES_NOT_SUPPORT_DRIVERUNLOAD_ROUTINE"></span>**IopLoadDriver:即插即用驱动程序** *xxxxxx* **不支持 DriverUnload 例程**  
名为的驱动程序*xxxxxx* IRP 支持\_MJ\_PNP，但未指定中的卸载例程**DriverEntry**。

<span id="DO_DEVICE_INITIALIZING_flag_not_cleared_on_DO_0x_________________nnnnnnnn"></span><span id="do_device_initializing_flag_not_cleared_on_do_0x_________________nnnnnnnn"></span><span id="DO_DEVICE_INITIALIZING_FLAG_NOT_CLEARED_ON_DO_0X_________________NNNNNNNN"></span>**不要\_设备\_正在初始化标记不清除上 0x** *nnnnnnnn*  
处的设备对象地址 0x*nnnnnnnn*创建外部**DriverEntry**，但\_设备\_返回到系统前未清除正在初始化位。

 

 





