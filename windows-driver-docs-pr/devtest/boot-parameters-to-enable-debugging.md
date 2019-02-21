---
title: 启用调试的启动参数
description: 启用调试的启动参数
ms.assetid: acbe2fcd-6f8f-49c8-9de6-1617a1723cf5
keywords:
- 引导参数 WDK
- 启动入口参数 WDK
- 内核调试支持 WDK 启动选项
- 本地调试 WDK 引导参数
- 单计算机调试 WDK 引导参数
- 电缆调试 WDK 引导参数
- IEEE 1394 电缆 WDK 引导参数
- 1394 连接 WDK 引导参数
- USB 2.0 调试连接 WDK 引导参数
- null 调制解调器电缆 WDK 引导参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6820f583a304421abca95cca26570bd4133e09db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519579"
---
# <a name="boot-parameters-to-enable-debugging"></a>启用调试的启动参数


## <span id="ddk_boot_parameters_to_enable_debugging_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_ENABLE_DEBUGGING_TOOLS"></span>


建立内核调试连接时，系统将提供对其执行内核调试器控制。 此外，当 bug 检查发生或内核模式程序与调试程序进行通信，计算机会等待响应的内核调试程序再继续执行。

有四种基本的调试方法，你可以配置使用的启动参数：

-   单计算机 （本地） 调试

-   使用调制解调器电缆进行调试

-   使用 IEEE 1394 电缆进行调试 （仅当目标计算机和主计算机都在运行 Microsoft Windows 7 或更高版本的 Windows）

-   使用 USB 2.0 调试电缆进行调试 （仅当目标计算机和主计算机都在运行 Microsoft Windows 7 或更高版本的 Windows）

### <a name="span-idbootoptionforlocaldebugginginwindowsvistaandlaterspanspan-idbootoptionforlocaldebugginginwindowsvistaandlaterspanboot-option-for-local-debugging-in-windows"></a><span id="boot_option_for_local_debugging_in_windows_vista_and_later"></span><span id="BOOT_OPTION_FOR_LOCAL_DEBUGGING_IN_WINDOWS_VISTA_AND_LATER"></span>用于在 Windows 中进行本地调试启动选项

若要启用内核调试在单台计算机上，使用 BCDEdit **/debug**启动选项。

若要使用 BCDEdit，使用提升的权限打开命令提示符窗口 (右键单击**命令提示符**然后单击**以管理员身份运行**从快捷菜单)。

**/Debug**选项具有以下语法：

```
bcdedit /debug [{ID}] { on | off }
```

**{**<em>ID</em>**}** GUID 关联的启动项。 如果 **{**<em>ID</em>**}** 未指定，则这些设置适用于当前启动项目。 以下命令将启用内核调试的当前 Windows 操作系统启动项目：

```
bcdedit /debug on
```

以下命令将启用内核调试的指定的 Windows 操作系统启动项目：

```
bcdedit /debug  {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

可以使用**bcdedit /enum**命令以查看当前启动项目和设置，并确定 GUID 与每个条目相关联。

有关更多详细信息，请参阅[ **BCDEdit /debug**](https://msdn.microsoft.com/library/windows/hardware/ff542191)。

### <a name="span-idbootoptionstodebugwithanullmodemcableinwindowsvistaandlatspanspan-idbootoptionstodebugwithanullmodemcableinwindowsvistaandlatspanboot-options-to-debug-with-a-null-modem-cable-in-windows"></a><span id="boot_options_to_debug_with_a_null_modem_cable_in_windows_vista_and_lat"></span><span id="BOOT_OPTIONS_TO_DEBUG_WITH_A_NULL_MODEM_CABLE_IN_WINDOWS_VISTA_AND_LAT"></span>在 Windows 中的调制解调器电缆与要调试的启动选项

若要启用调试，并在 Windows 中的调制解调器电缆，使用 BCDEdit 并设置调试连接类型设置为"序列"。 将此设置使用的全局[ **BCDEdit /dbgsettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542187)命令并后接**串行**，或将其设置为特定的启动项使用[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令并后接**debugtype 串行**。 此外必须使用[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)命令以启用内核调试全局或为所需的操作系统。

如果尚未使用 BCDEdit，将使用 COM1 和 115200 波特率串行通信的默认全局调试设置。

若要显示的当前设置，请使用以下命令：

```
bcdedit /dbgsettings

debugtype               Serial
debugport               1
baudrate                115200
```

若要使用 BCDEdit，使用提升的权限打开命令提示符窗口 (右键单击**命令提示符**然后单击**以管理员身份运行**从快捷菜单)。

若要设置为串行通信的全局调试设置，请使用以下语法：

**bcdedit /dbgsettings serial** \[ **debugport:**<em>port</em>\] \[ **baudrate:** *baud*\]

下面的示例演示如何指定串行通信为全局的调试设置。

```
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```

若要设置为特定的启动项，或当前项串行调试设置，请使用以下语法：

**bcdedit /set** \[ **{**<em>ID</em>**}** \] **debugtype 串行**

**bcdedit /set** \[**{**<em>ID</em>**}**\] **debugport** *port*

**bcdedit /set** \[**{**<em>ID</em>**}**\] **baudrate** *baud*

如果没有 **{**<em>ID</em>**}** 指定的设置适用于当前处于活动状态的启动项。

下面的示例演示如何指定特定的启动项的串行调试设置。 若要启用调试设置，必须重新启动计算机，然后选择已配置用于调试该启动项。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} debugtype serial
```

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} debugport 1
```

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} baudrate 115200
```

```
bcdedit /debug {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

可以使用**bcdedit /enum**命令查看当前启动项目和设置。

有关更多详细信息，请参阅[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)并[ **BCDEdit /dbgsettings**](https://msdn.microsoft.com/library/windows/hardware/ff542187)。

### <a name="span-idbootparameterstodebugwitha1394cableinwindowsvistaandlaterspanspan-idbootparameterstodebugwitha1394cableinwindowsvistaandlaterspanboot-parameters-to-debug-with-a-1394-cable-in-windows"></a><span id="boot_parameters_to_debug_with_a_1394_cable_in_windows_vista_and_later"></span><span id="BOOT_PARAMETERS_TO_DEBUG_WITH_A_1394_CABLE_IN_WINDOWS_VISTA_AND_LATER"></span>在 Windows 中的 1394年电缆与要调试的启动参数

若要启用使用 IEEE 1394 电缆在 Windows 中进行调试，使用 BCDEdit 并设置调试连接类型设置为"1394"。 将此设置使用的全局[ **BCDEdit /dbgsettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542187)命令并后接**1394年**，或将其设置为特定的启动项使用[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令并后接**debugtype 1394**。 此外必须使用[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)命令以启用内核调试全局或为所需的操作系统。

若要使用 BCDEdit，使用提升的权限打开命令提示符窗口 (右键单击**命令提示符**然后单击**以管理员身份运行**从快捷菜单)。

若要设置的调试设置 1394年全局范围内，使用以下语法：

**bcdedit /dbgsettings 1394** \[ **channel:**<em>channel</em> \]

下面的示例演示如何指定 1394年为全局的调试设置。

```
bcdedit /dbgsettings 1394 channel:32 
```

若要设置为特定的启动项，或当前项的 1394年调试设置，请使用以下语法：

**bcdedit /set** \[**{**<em>ID</em>**}**\] **debugtype 1394**

**bcdedit /set** \[**{**<em>ID</em>**}**\] **channel** *channel*

如果 **{**<em>ID</em>**}** 未指定，则这些设置适用于当前启动项目。

下面的示例演示如何指定一个特定的启动项的 1394年调试设置以及如何使用 **/debug**选项以启用该启动项的内核调试。 请注意，若要启用调试设置，必须重新启动计算机，然后选择已配置用于调试的启动项目。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} debugtype 1394
```

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} channel 32
```

```
bcdedit /debug {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

可以使用**bcdedit /enum**命令查看当前启动项目和设置。

有关更多详细信息，请参阅[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)并[ **BCDEdit /dbgsettings**](https://msdn.microsoft.com/library/windows/hardware/ff542187)。

### <a name="span-idbootparameterstodebugwithausb20debuggingcableinwindowsvisspanspan-idbootparameterstodebugwithausb20debuggingcableinwindowsvisspanboot-parameters-to-debug-with-a-usb-20-debugging-cable-in-windows"></a><span id="boot_parameters_to_debug_with_a_usb_2_0_debugging_cable_in_windows_vis"></span><span id="BOOT_PARAMETERS_TO_DEBUG_WITH_A_USB_2_0_DEBUGGING_CABLE_IN_WINDOWS_VIS"></span>使用 USB 2.0 调试电缆在 Windows 中进行调试的启动参数

若要启用使用 USB 电缆在这些版本的 Windows 中进行调试，使用 BCDEdit 并设置调试连接类型设置为"USB"。 将此设置使用的全局[ **BCDEdit /dbgsettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542187)命令并后接**usb**，或将其设置为特定的启动项使用[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令并后接**debugtype usb**。 此外必须使用[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)命令以启用内核调试全局或为所需的操作系统。

若要使用 BCDEdit，使用提升的权限打开命令提示符窗口 (右键单击**命令提示符**然后单击**以管理员身份运行**从快捷菜单)。

若要全局设置 USB 调试设置，请使用以下语法：

**bcdedit /dbgsettings usb** \[**targetname:**<em>name</em>\]

下面的示例演示如何指定 USB 为全局的调试设置。

```
bcdedit /dbgsettings usb targetname:U1
```

若要将调试设置 USB 设置特定的启动项，或当前项，使用以下语法：

**bcdedit /set** \[ **{**<em>ID</em>**}** \] **debugtype usb**

**bcdedit /set** \[**{**<em>ID</em>**}**\] **targetname** *name*\]

如果没有 **{**<em>ID</em>**}** 指定的设置适用于当前启动项目。

下面的示例演示如何指定 USB 调试设置特定的启动项，以及如何使用 **/debug**命令以启用该启动项的内核调试。 请注意，若要启用调试设置，必须重新启动计算机，然后选择已配置用于调试的启动项目。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} debugtype usb
```

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} targetname u2
```

```
bcdedit /debug {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

可以使用**bcdedit /enum**命令查看当前启动项目和设置。

有关更多详细信息，请参阅[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)并[ **BCDEdit /dbgsettings**](https://msdn.microsoft.com/library/windows/hardware/ff542187)。

### <a name="span-idbootparameterstodebugthebootprocessinwindowsvistaandlaterspanspan-idbootparameterstodebugthebootprocessinwindowsvistaandlaterspanboot-parameters-to-debug-the-boot-process-in-windows"></a><span id="boot_parameters_to_debug_the_boot_process_in_windows_vista_and_later"></span><span id="BOOT_PARAMETERS_TO_DEBUG_THE_BOOT_PROCESS_IN_WINDOWS_VISTA_AND_LATER"></span>若要调试在 Windows 中的启动进程的启动参数

若要启用启动调试，请使用[ **BCDEdit /bootdebug** ](https://msdn.microsoft.com/library/windows/hardware/ff542183)命令并指定相应的启动组件。 如果你想要执行内核调试 Windows 启动后，请使用[ **BCDEdit /debug** ](https://msdn.microsoft.com/library/windows/hardware/ff542191)也命令。

您还必须选择调试连接 (串行，1394年或 USB 2.0)。 这可以使用任一[ **BCDEdit /dbgsettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542187)或[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令，就像正常的内核调试一样。

有关更多详细信息，请参阅[ **BCDEdit /bootdebug**](https://msdn.microsoft.com/library/windows/hardware/ff542183)。

 

 





