---
title: 在 KMDF 驱动程序中使用 WPP 软件跟踪
description: 在 KMDF 驱动程序中使用 WPP 软件跟踪
ms.assetid: dad7aa8d-4ced-47b3-80d2-ec9cfb355783
keywords:
- 跟踪 WDK，基于框架的驱动程序软件
- 调试驱动程序 WDK KMDF 软件跟踪
- 跟踪 WDK，基于框架的驱动程序
- WPP 软件跟踪 WDK，基于框架的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75c7715187396c2e4f8ad34cf5acda990a49485
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372153"
---
# <a name="using-wpp-software-tracing-in-kmdf-drivers"></a>在 KMDF 驱动程序中使用 WPP 软件跟踪


[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)，可以添加跟踪消息，以帮助您调试您的驱动程序。 此外，框架的[事件记录器](using-the-framework-s-event-logger.md)提供了数百个您可以查看的跟踪消息。

可以通过查看跟踪消息[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)或[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)。 此外可以[将跟踪消息发送到内核调试程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)。

### <a name="adding-tracing-messages-to-your-driver"></a>将跟踪消息到您的驱动程序添加

若要将跟踪消息添加到您基于 framework 的驱动程序，必须：

- 添加 **\#包括**到每个驱动程序的源代码文件包含任何 WPP 宏指令。 此指令必须标识[跟踪消息标头 (TMH) 文件](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)。 文件名称的格式必须&lt;*驱动程序的源的文件名*&gt; **.tmh**。

  例如，如果您的驱动程序由两个源文件组成，称为*MyDriver1.c*并*MyDriver2.c*，然后*MyDriver1.c*必须包含：

  **\#include "MyDriver1.tmh"**

  并*MyDriver2.c*必须包含：

  **\#include "MyDriver2.tmh"**

  生成您在 Microsoft Visual Studio 中的驱动程序时，WPP 预处理器生成。*tmh*文件。

- 定义[WPP\_控制\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))标头文件中的宏。 此宏可定义 GUID 并[跟踪标志](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)用于驱动程序的跟踪的消息。

- 包括[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))您的驱动程序中的宏[ **DriverEntry 例程**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)。 此宏将激活软件驱动程序中的跟踪。

- 包括[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))您的驱动程序中的宏[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)回调函数。 此宏将停用软件驱动程序中的跟踪。

- 使用[ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏，或[自定义的版本](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)的驱动程序来创建跟踪消息中的宏。

- 打开您的驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择**属性**。 在驱动程序的属性页中，单击**配置属性**，然后**Wpp**。 下**常规**菜单中，设置**运行 WPP 跟踪**为是。 下**文件选项**菜单中，你还应指定框架的 WPP 模板文件，例如：

  ```cpp
  {km-WdfDefault.tpl}*.tmh
  ```
    
- 若要指定其他 WPP 跟踪设置为您的驱动程序项目在 Visual Studio 中，右键单击解决方案资源管理器中的驱动程序项目。 然后遵循该链接属性-> 配置属性-> WPP 跟踪。 

- 若要指定跟踪配置文件，请使用扫描配置数据设置。 为多个一个跟踪配置文件将其命令行下添加-> 附加选项，如下所示
  ```cpp
  -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\wdftraceenums.h"
  ```
  有关将跟踪消息添加到您的驱动程序的详细信息，请参阅[添加到驱动程序 WPP 宏](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>使用 WPP 软件跟踪的示例驱动程序

AMCC5933、 NONPNP、 KMDF\_FX2、 PCIDRV、 PLX9x5x 和序列[示例驱动程序](sample-kmdf-drivers.md)使用 WPP 软件跟踪。

 

 





