---
title: 已检验版本断点和消息
description: 已检验版本断点和消息
ms.assetid: 99b27487-eb95-4303-bad6-0b7ed8b450f0
keywords:
- 断点 WDK
- 检查生成 WDK，断点
- 已检查生成 WDK，消息
- 消息 WDK 检查版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ea732a5aae0ad45222e0332d18045a812794f47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840297"
---
# <a name="checked-build-breakpoints-and-messages"></a>已检验版本断点和消息


## <span id="ddk_checked_build_breakpoints_and_messages_tools"></span><span id="DDK_CHECKED_BUILD_BREAKPOINTS_AND_MESSAGES_TOOLS"></span>


本主题包含一个列表，并说明了驱动程序在选中的内部版本中可能会遇到的一些常见断点和[**DbgPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)消息。

<span id="____DPC_routine___1_sec_---_This_is_not_a_break_in_KeUpdateSystemTime"></span><span id="____dpc_routine___1_sec_---_this_is_not_a_break_in_keupdatesystemtime"></span><span id="____DPC_ROUTINE___1_SEC_---_THIS_IS_NOT_A_BREAK_IN_KEUPDATESYSTEMTIME"></span> **\*\*\* DPC 例程 &gt; 1 秒---这不是 KeUpdateSystemTime 中的一个中断**  
此消息紧接在发出断点之前出现。 它指示活动驱动程序在 DPC 例程中使用了超过1秒。

<span id="____isr_at_0x_________________nnnnnnnn_________________took_over_.5_second"></span><span id="____ISR_AT_0X_________________NNNNNNNN_________________TOOK_OVER_.5_SECOND"></span>**0x nnnnnnnn\* ISR 的\*\*** **花费了5秒**  
此消息紧接在发出断点之前出现。 它表示对入口点 0x*nnnnnnnn*执行的中断服务例程的执行时间超过了500毫秒。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________FAILED_TO_INITIALIZE___0XNNNNNNNN"></span>**IOINIT：内置驱动程序** *xxxxxx* **无法初始化− 0x * * * nnnnnnnn* ，名为*xxxxxx*的启动启动驱动程序*从其**nnnnnnnn**入口点返回了失败状态 0x DriverEntry *。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOINIT：内置驱动程序** *xxxxxx* **花**了**的初始化**  
在其**DriverEntry**入口点中，名为*xxxxxx*的启动启动驱动程序在*y z*秒（长度超过5秒的预期最大时间）内执行。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOINIT：内置驱动程序** *xxxxxx* **采取**了**的初始化失败**  
在其**DriverEntry**入口点中，名为*xxxxxx*的启动启动驱动程序在*y z*秒（长度超过5秒的预期最大时间）内执行。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOLOAD：驱动程序** *xxxxxx* **花**了**的初始化**  
名为*xxxxxx*的驱动程序在其**DriverEntry**入口点中执行了*y z*秒（长度超过5秒的预期最大时间）。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOLOAD：驱动程序** *xxxxxx* **采取**了**的初始化失败**  
名为*xxxxxx*的驱动程序在其**DriverEntry**入口点中执行了*y z*秒（长度超过5秒的预期最大时间）。

<span id="IopLoadDriver__A_PnP_driver__________________xxxxxx_________________does_not_support_DriverUnload_routine"></span><span id="ioploaddriver__a_pnp_driver__________________xxxxxx_________________does_not_support_driverunload_routine"></span><span id="IOPLOADDRIVER__A_PNP_DRIVER__________________XXXXXX_________________DOES_NOT_SUPPORT_DRIVERUNLOAD_ROUTINE"></span>**IopLoadDriver： PnP 驱动程序** *Xxxxxx*不**支持 DriverUnload 例程**  
名为*xxxxxx*的驱动程序支持 IRP\_MJ\_PNP，但未在**DriverEntry**中指定卸载例程。

<span id="DO_DEVICE_INITIALIZING_flag_not_cleared_on_DO_0x_________________nnnnnnnn"></span><span id="do_device_initializing_flag_not_cleared_on_do_0x_________________nnnnnnnn"></span><span id="DO_DEVICE_INITIALIZING_FLAG_NOT_CLEARED_ON_DO_0X_________________NNNNNNNN"></span> **\_设备\_在 DO 0x nnnnnnnn 上未清除的标记**  
在**DriverEntry**处创建了位于地址 0x*nnnnnnnn*的设备对象，但在返回到系统之前未清除 "DO\_设备\_初始化位"。

 

 





