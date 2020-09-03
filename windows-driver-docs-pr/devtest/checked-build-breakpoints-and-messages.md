---
title: 已检验版本断点和消息
description: 已检验版本断点和消息
ms.assetid: 99b27487-eb95-4303-bad6-0b7ed8b450f0
keywords:
- 断点 WDK
- 检查生成 WDK，断点
- 已检查生成 WDK，消息
- 消息 WDK 检查版本
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 963d0a2e8cd2ccff7d1e574dd39baa80a0fd42a5
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384763"
---
# <a name="checked-build-breakpoints-and-messages"></a>已检验版本断点和消息

## <span id="ddk_checked_build_breakpoints_and_messages_tools"></span><span id="DDK_CHECKED_BUILD_BREAKPOINTS_AND_MESSAGES_TOOLS"></span>

本主题包含一个列表，并说明了驱动程序在选中的内部版本中可能会遇到的一些常见断点和 [**DbgPrint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint) 消息。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

<span id="____DPC_routine___1_sec_---_This_is_not_a_break_in_KeUpdateSystemTime"></span><span id="____dpc_routine___1_sec_---_this_is_not_a_break_in_keupdatesystemtime"></span><span id="____DPC_ROUTINE___1_SEC_---_THIS_IS_NOT_A_BREAK_IN_KEUPDATESYSTEMTIME"></span>**\*\*\* DPC 例程 &gt; 1 秒---在 KeUpdateSystemTime 中不是一个中断**  
此消息紧接在发出断点之前出现。 它指示活动驱动程序在 DPC 例程中使用了超过1秒。

<span id="____isr_at_0x_________________nnnnnnnn_________________took_over_.5_second"></span><span id="____ISR_AT_0X_________________NNNNNNNN_________________TOOK_OVER_.5_SECOND"></span>0x *nnnnnnnn*上** \* \* \* 的 ISR** **耗时超过5秒**  
此消息紧接在发出断点之前出现。 它表示对入口点 0x*nnnnnnnn* 执行的中断服务例程的执行时间超过了500毫秒。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________FAILED_TO_INITIALIZE___0XNNNNNNNN"></span>**IOINIT：内置驱动程序** *xxxxxx* **无法初始化− 0x * * * nnnnnnnn* ，名为 *xxxxxx* 的启动启动驱动程序*从其 **nnnnnnnn** 入口点返回了失败状态 0x DriverEntry *。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOINIT：内置驱动程序** *xxxxxx* **花** *y.z*了**的初始化**  
名为 *xxxxxx* 的启动启动驱动程序在 *y z* 秒内执行， (超过5秒的预期最大时间) 其 **DriverEntry** 入口点。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOINIT：内置驱动程序** *xxxxxx* **采取** *y.z*了**的初始化失败**  
名为 *xxxxxx* 的启动启动驱动程序在 *y z* 秒内执行， (超过5秒的预期最大时间) 其 **DriverEntry** 入口点。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOLOAD：驱动程序** *xxxxxx* **花** *y.z*了**的初始化**  
名为 *xxxxxx* 的驱动程序执行的是 (的 *y z* 秒，其 **DriverEntry** 入口点) 的时间长度超过5秒的预期最大时间。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOLOAD：驱动程序** *xxxxxx* **采取** *y.z*了**的初始化失败**  
名为 *xxxxxx* 的驱动程序执行的是 (的 *y z* 秒，其 **DriverEntry** 入口点) 的时间长度超过5秒的预期最大时间。

<span id="IopLoadDriver__A_PnP_driver__________________xxxxxx_________________does_not_support_DriverUnload_routine"></span><span id="ioploaddriver__a_pnp_driver__________________xxxxxx_________________does_not_support_driverunload_routine"></span><span id="IOPLOADDRIVER__A_PNP_DRIVER__________________XXXXXX_________________DOES_NOT_SUPPORT_DRIVERUNLOAD_ROUTINE"></span>**IopLoadDriver： PnP 驱动程序** *Xxxxxx*不 **支持 DriverUnload 例程**  
名为 *xxxxxx* 的驱动程序支持 IRP \_ MJ \_ PNP，但未在 **DriverEntry**中指定卸载例程。

<span id="DO_DEVICE_INITIALIZING_flag_not_cleared_on_DO_0x_________________nnnnnnnn"></span><span id="do_device_initializing_flag_not_cleared_on_do_0x_________________nnnnnnnn"></span><span id="DO_DEVICE_INITIALIZING_FLAG_NOT_CLEARED_ON_DO_0X_________________NNNNNNNN"></span>**执行 \_\_在 DO 0x nnnnnnnn 上未清除设备初始化标志** *nnnnnnnn*  
在**DriverEntry**处创建了位于地址 0x*nnnnnnnn*的设备对象，但在 \_ \_ 返回到系统之前，未清除 "设备初始化" 位。

 

