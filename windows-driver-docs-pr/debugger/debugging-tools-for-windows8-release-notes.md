---
title: 调试工具的 Windows8 发行说明
description: 调试工具的 Windows8 发行说明
ms.assetid: 15776778-691F-4F76-92CE-2DB266AD31E8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1761adeaf561a6063544d0fdf9419ce6961f33f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533806"
---
# <a name="debugging-tools-for-windows8-release-notes"></a>调试工具的 Windows8 发行说明


## <a name="span-idchannelnumberfor1394debugginginvisualstudiospanspan-idchannelnumberfor1394debugginginvisualstudiospanspan-idchannelnumberfor1394debugginginvisualstudiospanchannel-number-for-1394-debugging-in-visual-studio"></a><span id="Channel_number_for_1394_debugging_in_Visual_Studio"></span><span id="channel_number_for_1394_debugging_in_visual_studio"></span><span id="CHANNEL_NUMBER_FOR_1394_DEBUGGING_IN_VISUAL_STUDIO"></span>用于 1394年调试在 Visual Studio 中的频道号


如果使用 Microsoft Visual Studio 来执行通过 1394年电缆的内核模式调试，则设置为 1 和 62 （含) 之间的十进制整数通道。 当您首次设置调试时，不要为 0 设置通道。 由于默认通道值为 0，软件假定存在不变，不会更新设置。 如果必须使用通道 0，第一次使用备用的通道 (1 至第 62)，然后切换到通道 0。

## <a name="span-idinlinefunctiondebuggingisonbydefaultspanspan-idinlinefunctiondebuggingisonbydefaultspanspan-idinlinefunctiondebuggingisonbydefaultspaninline-function-debugging-is-on-by-default"></a><span id="Inline_function_debugging_is_on_by_default"></span><span id="inline_function_debugging_is_on_by_default"></span><span id="INLINE_FUNCTION_DEBUGGING_IS_ON_BY_DEFAULT"></span>内联函数调试处于打开状态


在 Windows 8 中，调试内联函数是默认启用。 该命令 **.inline 0**关闭调试内联函数，和命令 **.inline 1**开启调试内联函数。

## <a name="span-idinvalidportnumberinconfigurationpagefornetworkdebuggingspanspan-idinvalidportnumberinconfigurationpagefornetworkdebuggingspanspan-idinvalidportnumberinconfigurationpagefornetworkdebuggingspaninvalid-port-number-in-configuration-page-for-network-debugging"></a><span id="Invalid_port_number_in_configuration_page_for_network_debugging"></span><span id="invalid_port_number_in_configuration_page_for_network_debugging"></span><span id="INVALID_PORT_NUMBER_IN_CONFIGURATION_PAGE_FOR_NETWORK_DEBUGGING"></span>在配置页中用于网络调试无效端口号


**问题：** 如果内核模式网络调试的情况下，端口号无效输入的配置页，配置成功，但主机计算机上的调试器无法连接到目标计算机。

**解决方法：** 请确保端口号无效。 有效的端口号范围是从 49152 – 65535。 此外，你的公司可能可以在其使用端口进行网络调试的限制。 若要确保输入有效的端口号，请检查您的内部 IP 安全策略。

## <a name="span-iduseofremotetoolincommandlinespanspan-iduseofremotetoolincommandlinespanuse-of-remote-tool-in-command-line"></a><span id="use_of_.remote_tool_in_command_line"></span><span id="USE_OF_.REMOTE_TOOL_IN_COMMAND_LINE"></span>使用命令行中的.remote 工具


**问题：** 利用 **.remote**中命令行工具创建旧样式 remote.exe 使用 npipe 崩溃接口。

**解决方法：** 使用 **.server**命令。

## <a name="span-iddesignfeaturesforvisualstudiospanspan-iddesignfeaturesforvisualstudiospanspan-iddesignfeaturesforvisualstudiospandesign-features-for-visual-studio"></a><span id="Design_features_for_Visual_Studio"></span><span id="design_features_for_visual_studio"></span><span id="DESIGN_FEATURES_FOR_VISUAL_STUDIO"></span>Visual Studio 的设计功能


-   一台计算机的自动预配包括用户模式和内核模式下启动，而不考虑其选择一个。 这需要两个预配为重新启动并需要 8 – 20 分钟。
-   对附加一次只有一个进程的支持。
-   在 Windows 调试器扩展的 Visual Studio 中调试会话，期间使用命令行管理异常。

## <a name="span-idglobaldesignfeaturesspanspan-idglobaldesignfeaturesspanspan-idglobaldesignfeaturesspanglobal-design-features"></a><span id="Global_design_features"></span><span id="global_design_features"></span><span id="GLOBAL_DESIGN_FEATURES"></span>全局设计功能


-   用户必须在提升的上下文中运行才能安装 USB 3.0 XHCI 筛选器驱动程序。 如果用户未在运行提升的权限，即插即用管理器将返回错误消息，不会通知用户提升是问题所在。
-   如果启用内核调试，则用于内核调试的设备应不是从系统中删除该设备仍然打开时。 如果删除该设备，系统将会挂起，将需要重新启动。

 

 





