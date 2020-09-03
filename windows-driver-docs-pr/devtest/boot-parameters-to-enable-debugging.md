---
title: 用于启用调试的启动参数
description: 用于启用调试的启动参数
ms.assetid: acbe2fcd-6f8f-49c8-9de6-1617a1723cf5
keywords:
- 启动参数 WDK
- 启动项参数 WDK
- 内核调试支持 WDK 启动选项
- 本地调试 WDK 启动参数
- 单计算机调试 WDK 启动参数
- 数据调试 WDK 启动参数
- IEEE 1394 电缆 WDK 启动参数
- 1394连接 WDK 启动参数
- USB 2.0 调试连接 WDK 启动参数
- 空调制解调器电缆 WDK 启动参数
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 262bbda6a8df10df8b6d8c3c3d8d92153ca9c842
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384361"
---
# <a name="boot-parameters-to-enable-debugging"></a>用于启用调试的启动参数


## <span id="ddk_boot_parameters_to_enable_debugging_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_ENABLE_DEBUGGING_TOOLS"></span>


建立内核调试连接时，系统会向内核调试器控制其执行。 此外，当发生 bug 检查或内核模式程序与调试器通信时，计算机会等待内核调试器的响应，然后再继续。

可以使用启动参数配置四种基本调试方法：

- 单台计算机 (本地) 调试

- 使用空调缆线进行调试

- 仅当目标计算机和主计算机运行的是 Microsoft Windows 7 或更高版本的 Windows 时，使用 IEEE 1394 电缆进行调试 () 

- 仅当目标计算机和主计算机运行的是 Microsoft Windows 7 或更高版本的 Windows 时，使用 USB 2.0 调试电缆进行调试 () 

### <a name="span-idboot_option_for_local_debugging_in_windows_vista_and_laterspanspan-idboot_option_for_local_debugging_in_windows_vista_and_laterspanboot-option-for-local-debugging-in-windows"></a><span id="boot_option_for_local_debugging_in_windows_vista_and_later"></span><span id="BOOT_OPTION_FOR_LOCAL_DEBUGGING_IN_WINDOWS_VISTA_AND_LATER"></span>用于在 Windows 中进行本地调试的启动选项

若要在一台计算机上启用内核调试，请使用 BCDEdit **/debug** boot 选项。

若要使用 BCDEdit，请使用提升的权限打开命令提示符窗口， (选择并按住或右键单击 **命令提示符** ，然后从快捷菜单中选择 "以 **管理员身份运行** ") 。

**/Debug**选项具有以下语法：

```console
bcdedit /debug [{ID}] { on | off }
```

**{**<em>Id</em>**}** 是与启动项关联的 ID，如默认 OS 启动项的 {默认}。 如果未指定 **{**<em>ID</em>**}**，则该命令将修改当前处于活动状态的操作系统。 有关使用启动条目标识符的详细信息，请参阅 [启动选项标识符](boot-options-identifiers.md)。

以下命令对当前 Windows 操作系统启动条目启用内核调试：

```console
bcdedit /debug on
```

可以使用 **bcdedit/enum** 命令查看当前启动项及其设置。

有关更多详细信息，请参阅 [**BCDEdit/debug**](./bcdedit--debug.md)。

### <a name="span-idboot_options_to_debug_with_a_null_modem_cable_in_windows_vista_and_latspanspan-idboot_options_to_debug_with_a_null_modem_cable_in_windows_vista_and_latspanboot-options-to-debug-with-a-null-modem-cable-in-windows"></a><span id="boot_options_to_debug_with_a_null_modem_cable_in_windows_vista_and_lat"></span><span id="BOOT_OPTIONS_TO_DEBUG_WITH_A_NULL_MODEM_CABLE_IN_WINDOWS_VISTA_AND_LAT"></span>在 Windows 中使用空调制网线进行调试的启动选项

若要在 Windows 中使用空调制网线启用调试，请使用 BCDEdit 并将 "调试" 连接类型设置为 "串行"。 你可以通过使用后跟**串行**的[**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)命令来全局设置此项，也可以使用后跟**debugtype 序列**的[**bcdedit/set**](./bcdedit--set.md)命令为特定启动项设置此项。 还必须使用 [**BCDEdit/debug**](./bcdedit--debug.md) 命令来启用对所需操作系统的内核调试。

如果未使用 BCDEdit，则默认的全局调试设置用于串行通信，使用 COM1，波特率为115200。

若要显示当前设置，请使用以下命令：

```console
bcdedit /dbgsettings

debugtype               Serial
debugport               1
baudrate                115200
```

若要使用 BCDEdit，请使用提升的权限打开命令提示符窗口， (选择并按住或右键单击 **命令提示符** ，然后从快捷菜单中选择 "以 **管理员身份运行** ") 。

若要将全局调试设置设置为串行通信，请使用以下语法：

**bcdedit/dbgsettings 串行** \[**debugport：**<em>端口</em> \] \[ **波特率：** *波特*\]

下面的示例演示如何将串行通信指定为全局调试设置。

```console
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```

若要将特定启动项的调试设置设置为串行，或将其设置为当前项，请使用以下语法：

**bcdedit/set** \[**{**<em>ID</em>**}** \]**debugtype 串行**

**bcdedit/set** \[**{**<em>ID</em>**}** \]**debugport** *端口*

**bcdedit/set** \[**{**<em>ID</em>**}** \]**波特率***波特*

如果未指定 **{**<em>ID</em>**}** ，则这些设置将应用于当前处于活动状态的启动条目。

下面的示例演示如何为默认启动项指定串行调试设置。 若要启用调试设置，必须重新启动计算机，然后选择已配置为进行调试的启动项。

```console
bcdedit /set debugtype serial
```

```console
bcdedit /set debugport 1
```

```console
bcdedit /set baudrate 115200
```

```console
bcdedit /debug on
```

可以使用 **bcdedit/enum** 命令查看当前启动项及其设置。

有关更多详细信息，请参阅 [**bcdedit/debug**](./bcdedit--debug.md) 和 [**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)。

### <a name="span-idboot_parameters_to_debug_with_a_1394_cable_in_windows_vista_and_laterspanspan-idboot_parameters_to_debug_with_a_1394_cable_in_windows_vista_and_laterspanboot-parameters-to-debug-with-a-1394-cable-in-windows"></a><span id="boot_parameters_to_debug_with_a_1394_cable_in_windows_vista_and_later"></span><span id="BOOT_PARAMETERS_TO_DEBUG_WITH_A_1394_CABLE_IN_WINDOWS_VISTA_AND_LATER"></span>使用 Windows 中的1394电缆进行调试的启动参数

若要使用 Windows 中的 IEEE 1394 电缆进行调试，请使用 BCDEdit 并将 "调试" 连接类型设置为 "1394"。 你可以使用后跟**1394**的[**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)命令全局设置此项，也可以使用后跟**debugtype 1394**的[**bcdedit/set**](./bcdedit--set.md)命令为特定启动项设置此项。 还必须使用 [**BCDEdit/debug**](./bcdedit--debug.md) 命令来启用对所需操作系统的内核调试。

若要使用 BCDEdit，请使用提升的权限打开命令提示符窗口， (选择并按住或右键单击 **命令提示符** ，然后从快捷菜单中选择 "以 **管理员身份运行** ") 。

若要将调试设置全局设置为1394，请使用以下语法：

**bcdedit/dbgsettings 1394** \[**通道：**<em>通道</em>\]

下面的示例演示如何指定1394作为全局调试设置。

```console
bcdedit /dbgsettings 1394 channel:32 
```

若要为特定启动项或当前项将调试设置设置为1394，请使用以下语法：

**bcdedit/set** \[**{**<em>ID</em>**}** \]**debugtype 1394**

**bcdedit/set** \[**{**<em>ID</em>**}** \]**通道***通道*

如果未指定 **{**<em>ID</em>**}** ，则这些设置将应用于当前启动项。

下面的示例演示如何为特定启动项指定1394调试设置，以及如何使用 **/debug** 选项为默认启动项启用内核调试。 请注意，若要启用调试设置，必须重新启动计算机，然后选择已配置为进行调试的启动项。

```console
bcdedit /set debugtype 1394
```

```console
bcdedit /set channel 32
```

```console
bcdedit /debug on
```

可以使用 **bcdedit/enum** 命令查看当前启动项及其设置。

有关更多详细信息，请参阅 [**bcdedit/debug**](./bcdedit--debug.md) 和 [**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)。

### <a name="span-idboot_parameters_to_debug_with_a_usb_2_0_debugging_cable_in_windows_visspanspan-idboot_parameters_to_debug_with_a_usb_2_0_debugging_cable_in_windows_visspanboot-parameters-to-debug-with-a-usb-20-debugging-cable-in-windows"></a><span id="boot_parameters_to_debug_with_a_usb_2_0_debugging_cable_in_windows_vis"></span><span id="BOOT_PARAMETERS_TO_DEBUG_WITH_A_USB_2_0_DEBUGGING_CABLE_IN_WINDOWS_VIS"></span>在 Windows 中使用 USB 2.0 调试电缆进行调试的启动参数

若要在这些版本的 Windows 中使用 USB 电缆启用调试，请使用 BCDEdit 并将 "调试" 连接类型设置为 "USB"。 可以使用后跟**usb**的[**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)命令全局设置此项，也可以使用后跟**debugtype usb**的[**bcdedit/set**](./bcdedit--set.md)命令为特定启动项设置此项。 还必须使用 [**BCDEdit/debug**](./bcdedit--debug.md) 命令来启用对所需操作系统的内核调试。

若要使用 BCDEdit，请使用提升的权限打开命令提示符窗口， (选择并按住或右键单击 **命令提示符** ，然后从快捷菜单中选择 "以 **管理员身份运行** ") 。

若要为 USB 全局设置调试设置，请使用以下语法：

**bcdedit/dbgsettings usb** \[**targetname：**<em>名称</em>\]

下面的示例演示如何将 USB 指定为全局调试设置。

```console
bcdedit /dbgsettings usb targetname:U1
```

若要为特定启动项或当前项将调试设置设置为 USB，请使用以下语法：

**bcdedit/set** \[**{**<em>ID</em>**}** \]**debugtype usb**

**bcdedit/set** \[**{**<em>ID</em>**}** \]**targetname** *名称*\]

如果未指定 **{**<em>ID</em>**}** ，则这些设置将应用于当前启动项。

下面的示例演示如何为特定启动项指定 USB 调试设置，以及如何使用 **/debug** 命令为默认启动项启用内核调试。 请注意，若要启用调试设置，必须重新启动计算机，然后选择已配置为进行调试的启动项。

```console
bcdedit /set debugtype usb
```

```console
bcdedit /set targetname u2
```

```console
bcdedit /debug on
```

可以使用 **bcdedit/enum** 命令查看当前启动项及其设置。

有关更多详细信息，请参阅 [**bcdedit/debug**](./bcdedit--debug.md) 和 [**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)。

### <a name="span-idboot_parameters_to_debug_the_boot_process_in_windows_vista_and_laterspanspan-idboot_parameters_to_debug_the_boot_process_in_windows_vista_and_laterspanboot-parameters-to-debug-the-boot-process-in-windows"></a><span id="boot_parameters_to_debug_the_boot_process_in_windows_vista_and_later"></span><span id="BOOT_PARAMETERS_TO_DEBUG_THE_BOOT_PROCESS_IN_WINDOWS_VISTA_AND_LATER"></span>用于在 Windows 中调试启动过程的启动参数

若要启用启动调试，请使用 [**BCDEdit/bootdebug**](./bcdedit--bootdebug.md) 命令，并指定相应的启动组件。 如果要在 Windows 启动后执行内核调试，还应使用 [**BCDEdit/debug**](./bcdedit--debug.md) 命令。

还必须选择 (串行、1394或 USB) 的调试连接。 可以通过 [**BCDEdit/dbgsettings**](./bcdedit--dbgsettings.md) 或 [**bcdedit/set**](./bcdedit--set.md) 命令完成此操作，就像在正常内核调试中一样。

有关更多详细信息，请参阅 [**BCDEdit/bootdebug**](./bcdedit--bootdebug.md)。