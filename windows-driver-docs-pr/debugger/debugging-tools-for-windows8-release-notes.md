---
title: Windows 8 调试工具发行说明
description: Windows 8 调试工具发行说明
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7acbba7b33855dc32df110c605d04a89e455ebd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819845"
---
# <a name="debugging-tools-for-windows8-release-notes"></a>Windows 8 调试工具发行说明


## <a name="span-idchannel_number_for_1394_debugging_in_visual_studiospanspan-idchannel_number_for_1394_debugging_in_visual_studiospanspan-idchannel_number_for_1394_debugging_in_visual_studiospanchannel-number-for-1394-debugging-in-visual-studio"></a><span id="Channel_number_for_1394_debugging_in_Visual_Studio"></span><span id="channel_number_for_1394_debugging_in_visual_studio"></span><span id="CHANNEL_NUMBER_FOR_1394_DEBUGGING_IN_VISUAL_STUDIO"></span>Visual Studio 中用于1394调试的通道号


如果使用 Microsoft Visual Studio 通过1394电缆执行内核模式调试，请将通道设置为介于1到62（含）之间的十进制整数。 首次设置调试时，不要将通道设置为0。 由于默认通道值为0，因此软件会假定不存在更改，也不会更新设置。 如果必须使用通道0，请首先使用备用通道 (1 到 62) ，然后切换到通道0。

## <a name="span-idinline_function_debugging_is_on_by_defaultspanspan-idinline_function_debugging_is_on_by_defaultspanspan-idinline_function_debugging_is_on_by_defaultspaninline-function-debugging-is-on-by-default"></a><span id="Inline_function_debugging_is_on_by_default"></span><span id="inline_function_debugging_is_on_by_default"></span><span id="INLINE_FUNCTION_DEBUGGING_IS_ON_BY_DEFAULT"></span>内联函数调试默认情况下启用


在 Windows 8 中，内联函数的调试默认情况下处于打开状态。 命令 **inline 0** 会关闭内联函数调试，而命令 **inline 1** 则启用内联函数调试。

## <a name="span-idinvalid_port_number_in_configuration_page_for_network_debuggingspanspan-idinvalid_port_number_in_configuration_page_for_network_debuggingspanspan-idinvalid_port_number_in_configuration_page_for_network_debuggingspaninvalid-port-number-in-configuration-page-for-network-debugging"></a><span id="Invalid_port_number_in_configuration_page_for_network_debugging"></span><span id="invalid_port_number_in_configuration_page_for_network_debugging"></span><span id="INVALID_PORT_NUMBER_IN_CONFIGURATION_PAGE_FOR_NETWORK_DEBUGGING"></span>用于网络调试的配置页中的端口号无效


**问题：** 如果在配置页中为内核模式网络调试输入了无效的端口号，则配置会成功，但主计算机上的调试器无法连接到目标计算机。

**解决方法：** 请确保端口号有效。 有效端口号范围为49152–65535。 此外，公司可能对可用于网络调试的端口有限制。 若要确保输入了有效的端口号，请检查内部 IP 安全策略。

## <a name="span-iduse_of_remote_tool_in_command_linespanspan-iduse_of_remote_tool_in_command_linespanuse-of-remote-tool-in-command-line"></a><span id="use_of_.remote_tool_in_command_line"></span><span id="USE_OF_.REMOTE_TOOL_IN_COMMAND_LINE"></span>在命令行中使用远程工具


**问题：** 使用 npipe 时，命令行中的 **远程** 工具会崩溃接口，因为它使用创建旧样式 remote.exe。

**解决方法：** 改为使用 **server** 命令。

## <a name="span-iddesign_features_for_visual_studiospanspan-iddesign_features_for_visual_studiospanspan-iddesign_features_for_visual_studiospandesign-features-for-visual-studio"></a><span id="Design_features_for_Visual_Studio"></span><span id="design_features_for_visual_studio"></span><span id="DESIGN_FEATURES_FOR_VISUAL_STUDIO"></span>Visual Studio 的设计功能


-   计算机的自动预配包括用户模式和内核模式引导，无论选择哪一种。 这要求预配两次，并需要8到20分钟。
-   支持一次仅附加一个进程。
-   在 Visual Studio 的 Windows 调试器扩展中调试会话期间，使用命令行管理异常。

## <a name="span-idglobal_design_featuresspanspan-idglobal_design_featuresspanspan-idglobal_design_featuresspanglobal-design-features"></a><span id="Global_design_features"></span><span id="global_design_features"></span><span id="GLOBAL_DESIGN_FEATURES"></span>全局设计功能


-   用户必须在提升的上下文中运行，才能安装 USB 3.0 XHCI 筛选器驱动程序。 如果用户未在提升的状态下运行，则 PnP 管理器会返回一条错误消息，该消息不会通知用户提升是否是问题。
-   如果启用内核调试，则当设备仍处于打开状态时，不应将用于内核调试的设备从系统中删除。 如果删除了设备，系统会挂起，需要重新启动。

 

 





