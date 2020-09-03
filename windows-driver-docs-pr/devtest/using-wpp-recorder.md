---
title: '用于日志记录跟踪的即时 Trace 录像机 (IFR) '
description: 即时 Trace 录像机 (IFR) 使跟踪提供程序（如内核模式驱动程序）可以在缓冲区中记录跟踪日志并存储 WPP 日志消息。
ms.assetid: D11FA28E-3B0C-4D9D-AEDA-8A80DE58091C
ms.date: 03/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 35aba4444ff54680620c3f43c8ef4995f4289f14
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385079"
---
# <a name="inflight-trace-recorder-ifr-for-logging-traces"></a>用于日志记录跟踪的即时 Trace 录像机 (IFR) 


*即时 Trace 录像机 (IFR) * 是一项跟踪功能，它允许跟踪提供程序（如内核模式驱动程序或 UMDF 驱动程序）创建一组内存中循环缓冲区，其中保留了最新的日志消息。 可以使用调试器查看日志消息。

IFR 是在 [WPP 软件跟踪](wpp-software-tracing.md)之上构建的。 IFR 通过 WPP 的主要优点是它自动开启，无需提前启动跟踪会话。

**适用于：**

-   最小 OS：适用于 KMDF 和 WDM 驱动程序开发人员的 Windows 8
-   最低操作系统： Windows 10 for UMDF (2.15) 驱动程序开发人员

## <a name="how-to-enable-inflight-trace-recorder-in-visual-studio"></a>如何在 Visual Studio 中启用即时 Trace 记录器

首先，请按照向 [Windows 驱动程序添加 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)中的步骤操作。

接下来，在项目属性页的 " **配置属性->WPP 跟踪->函数和宏 >选项**" 下，选择 **"是"**。

最后，仅对于 UMDF，还需要执行一个额外的步骤：在 **WPP 跟踪->函数和宏选项->预处理器定义**中添加 `WPP_MACRO_USE_KM_VERSION_FOR_UM=1` 。


## <a name="how-to-enable-inflight-trace-recorder-from-the-command-line"></a>如何从命令行启用即时 Trace 记录器

如果手动编辑 .vcxproj 文件，请设置以下项：

对于 KMDF 或 WDM 驱动程序：

```xml
    <ClCompile Include=...>
        <WppEnabled>true</WppEnabled>
        <WppKernelMode>true</WppKernelMode>
        <WppRecorderEnabled>true</WppRecorderEnabled>
        ...
    </ClCompile>
```

对于 UMDF 驱动程序：

```xml
    <ClCompile Include=...>
        <WppEnabled>true</WppEnabled>
        <WppRecorderEnabled>true</WppRecorderEnabled>
        <WppPreprocessorDefinitions>WPP_MACRO_USE_KM_VERSION_FOR_UM=1</WppPreprocessorDefinitions>
        ...
    </ClCompile>
```


## <a name="how-to-send-trace-messages-to-the-default-log"></a>如何将跟踪消息发送到默认日志

按照向 [Windows 驱动程序添加 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)中的说明进行操作。  例如：

 - 在 [*DriverEntry*](../wdf/driverentry-for-kmdf-drivers.md)中调用 `WPP_INIT_TRACING(DriverObject, RegistryPath)` 。
 - 在 [*EvtDriverUnload*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)中调用 `WPP_CLEANUP(WdfDriverWdmGetDriverObject(Driver))` 。

现在，驱动程序可以根据需要随时调用 trace 函数。 例如：`TraceEvents(TRACE_LEVEL_ERROR, DBG_INIT, "WdfDriverCreate failed, %!STATUS!", ntStatus);`

有关详细信息，请参阅 [WPP_INIT_TRACING](/previous-versions/windows/hardware/drivers/ff556193(v=vs.85)) 和 [WPP_CLEANUP](/previous-versions/windows/hardware/drivers/ff556183(v=vs.85))。

## <a name="how-to-send-trace-messages-to-a-custom-log"></a>如何将跟踪消息发送到自定义日志

这仅适用于 (KMDF 或 WDM) 的内核模式驱动程序。

对于大多数驱动程序，单个默认日志就足够了。 但是，在某些情况下，为不同的实体使用单独的日志缓冲区会很有帮助。

例如，在编写总线驱动程序时，您可能希望每个子设备都具有自己的缓冲区。 然后，可以使用调试器只转储特定子设备的日志。

若要设置自定义日志，驱动程序必须包括 `<WppRecorder.h>` 。 然后调用以下 Api：

 - [**WppRecorderLogCreate**](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate) 创建多个日志缓冲区
 - [**WppRecorderLogDelete**](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogdelete) 调用 **WPP_CLEANUP**。
 - [**WppRecorderLogSetIdentifier**](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogsetidentifier) 设置给定记录器日志的字符串标识符 (可选) 
 - [**WppRecorderConfigure**](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure) 若要禁用默认日志 (可选) 

驱动程序还需要定义一个将日志句柄用作第一个参数的新跟踪宏。 有关示例，请参阅 [Toaster 示例驱动程序](https://github.com/microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured/trace.h)。


## <a name="how-to-view-trace-messages-in-the-debugger"></a>如何在调试器中查看跟踪消息

对于 KMDF 和 UMDF 驱动程序，请使用 [**wdfkd wdflogdump**](../debugger/-wdfkd-wdflogdump.md) 。 它将打印框架 IFR 日志和驱动程序 IFR 日志。

对于 WDM 驱动程序，请使用[**！ rcdrkd. rcdrloglist**](../debugger/-rcdrkd-rcdrloglist.md)和[**！ rcdrkd。**](../debugger/-rcdrkd-rcdrlogdump.md)


## <a name="configure-inflight-trace-recorder-parameters"></a>配置即时跟踪记录器参数

可以在驱动程序的 [参数密钥](../wdf/introduction-to-registry-keys-for-drivers.md)下配置 IFR。

使用以下注册表值：

**LogPages： REG_DWORD**

设置为存储默认日志的页数。 默认值为1。

**VerboseOn： REG_DWORD**

默认设置为零会导致 IFR 记录错误、警告和信息事件。 设置为 one 可将详细输出添加到日志中。