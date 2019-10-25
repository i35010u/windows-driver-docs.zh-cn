---
title: 在 KMDF 驱动程序中使用 WPP 软件跟踪
description: 在 KMDF 驱动程序中使用 WPP 软件跟踪
ms.assetid: dad7aa8d-4ced-47b3-80d2-ec9cfb355783
keywords:
- 软件跟踪 WDK，基于框架的驱动程序
- 调试驱动程序 WDK KMDF、软件跟踪
- 跟踪 WDK，基于框架的驱动程序
- WPP 软件跟踪 WDK，基于框架的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a167a01eecab1067a71a7a3c38ea15e7c7161551
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831934"
---
# <a name="using-wpp-software-tracing-in-kmdf-drivers"></a>在 KMDF 驱动程序中使用 WPP 软件跟踪


通过[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)，你可以添加跟踪消息，以帮助你调试驱动程序。 此外，框架的[事件记录器](using-the-framework-s-event-logger.md)提供数以百计的跟踪消息，您可以查看这些消息。

您可以通过使用[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)或[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)来查看跟踪消息。 你还可以向[内核调试器发送跟踪消息](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)。

### <a name="adding-tracing-messages-to-your-driver"></a>向驱动程序添加跟踪消息

若要将跟踪消息添加到基于框架的驱动程序，必须执行以下操作：

- 将 **\#include**指令添加到每个包含任何 WPP 宏的驱动程序源文件中。 此指令必须标识[跟踪消息标头（TMH）文件](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)。 文件名的格式必须为 &lt;*驱动程序名*&gt;**tmh**。

  例如，如果驱动程序包含两个源文件（称为*mydriver1.inf*和*mydriver2.inf 会被*），则*mydriver1.inf*必须包含：

  **\#包括 "tmh"**

  和*mydriver2.inf 会被*必须包含：

  **\#包括 "tmh"**

  在 Microsoft Visual Studio 中生成驱动程序时，WPP 预处理器会生成。*tmh*文件。

- 在标头文件中定义一个[WPP\_控件\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏。 此宏为驱动程序的跟踪消息定义 GUID 和[跟踪标志](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)。

- 在驱动程序的[**DriverEntry 例程**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)中包括[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏。 此宏激活驱动程序中的软件跟踪。

- 在驱动程序的[*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)回调函数中包括[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))宏。 此宏停用驱动程序中的软件跟踪。

- 使用驱动程序中的[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏或宏的[自定义版本](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)来创建跟踪消息。

- 打开驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择“属性”。 在驱动程序的属性页中，单击 "**配置属性**"，然后单击 " **Wpp**"。 在 "**常规**" 菜单下，将 "**运行 WPP 跟踪**" 设置为 "是"。 在 "**文件选项**" 菜单下，还应指定框架的 WPP 模板文件，例如：

  ```cpp
  {km-WdfDefault.tpl}*.tmh
  ```
    
- 若要在 Visual Studio 中为驱动程序项目指定附加的 WPP 跟踪设置，请在解决方案资源管理器中右键单击驱动程序项目。 然后，按照 "属性" 链接-> 配置属性-> WPP 跟踪。 

- 若要指定跟踪配置文件，请使用 "扫描配置数据" 设置。 对于多个跟踪配置文件，请将其添加到 "命令行" 下 > "其他选项"，如下所示
  ```cpp
  -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\wdftraceenums.h"
  ```
  有关将跟踪消息添加到驱动程序的详细信息，请参阅向[驱动程序添加 WPP 宏](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>使用 WPP 软件跟踪的示例驱动程序

AMCC5933、NONPNP、KMDF\_FX2、PCIDRV、PLX9x5x 和串行[示例驱动程序](sample-kmdf-drivers.md)使用 WPP 软件跟踪。

 

 





