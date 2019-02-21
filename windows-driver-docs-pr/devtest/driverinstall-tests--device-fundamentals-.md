---
title: 驱动程序安装测试（设备基础功能）
description: 测试类别包括测试，卸载并重新安装驱动程序若干次以测试驱动程序安装安装的功能。
ms.assetid: 3FC00D4B-6520-45F1-805C-A5F8B6AACAC8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eedcb75a749a1e843b34c806be59cf0a49414112
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542369"
---
# <a name="driver-install-tests-device-fundamentals"></a>驱动程序安装测试（设备基础功能）


测试类别包括测试，卸载并重新安装驱动程序若干次以测试驱动程序安装安装的功能。 测试启动 I/O 在每个重新安装后针对驱动程序和设备的测试。 测试旨在改进最终用户需要安装和重新安装设备驱动程序或设备的总体体验。

## <a name="span-iddriverinstalltestsspanspan-iddriverinstalltestsspandriverinstall-tests"></a><span id="driverinstall_tests"></span><span id="DRIVERINSTALL_TESTS"></span>DriverInstall 测试


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">测试</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Reinstall_with_IO_Before_and_After"></span><span id="reinstall_with_io_before_and_after"></span><span id="REINSTALL_WITH_IO_BEFORE_AND_AFTER"></span>之前和之后重新安装与 IO</p></td>
<td align="left"><p>此测试卸载和重新安装所选设备的驱动程序并运行测试的设备上的 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_Reinstall_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>Reinstall_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idaboutthereinstallwithiobeforeandaftertestspanspan-idaboutthereinstallwithiobeforeandaftertestspanspan-idaboutthereinstallwithiobeforeandaftertestspanabout-the-reinstall-with-io-before-and-after-test"></a><span id="About_the_ReInstall_with_I_O_Before_and_After_test"></span><span id="about_the_reinstall_with_i_o_before_and_after_test"></span><span id="ABOUT_THE_REINSTALL_WITH_I_O_BEFORE_AND_AFTER_TEST"></span>有关重新安装与 I/O 之前和之后测试


此测试将执行以下操作：

1.  验证测试设备及其子代未报告任何设备问题代码。
2.  在测试设备和使用 WDTF 简单 I/O 插件及其后代上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://msdn.microsoft.com/library/windows/hardware/hh781398)有关详细信息。
3.  将原始的驱动程序测试设备上重新安装[ **IWDTFDriverSetupAction2::UpdateDriver** ](https://msdn.microsoft.com/library/windows/hardware/hh450945)方法。
4.  验证测试设备及其子代未报告任何设备问题代码。
5.  在测试设备和使用 WDTF 简单 I/O 插件及其后代上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://msdn.microsoft.com/library/windows/hardware/hh781398)有关详细信息。
6.  如果重新启动系统步骤\#3 需要重新启动。
7.  测试设备上安装为 NULL 的驱动程序[ **IWDTFDriverSetupAction2::UnInstallDriverPermanently** ](https://msdn.microsoft.com/library/windows/hardware/hh450941)方法重新启动系统，如果需要重新启动。
8.  在测试使用的设备上重新安装原始驱动程序[ **IWDTFDriverSetupAction2::UpdateDriver** ](https://msdn.microsoft.com/library/windows/hardware/hh450945)方法。
9.  验证测试设备及其子代未报告任何设备问题代码。
10. 在测试设备和使用 WDTF 简单 I/O 插件及其后代上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://msdn.microsoft.com/library/windows/hardware/hh781398)有关详细信息。
11. 重复步骤 1-10 几次。

### <a name="span-iddebuginstallationfailuresusingthesetupapilogsspanspan-iddebuginstallationfailuresusingthesetupapilogsspanspan-iddebuginstallationfailuresusingthesetupapilogsspandebug-installation-failures-using-the-setup-api-logs"></a><span id="Debug_installation_failures_using_the_Setup_API_logs"></span><span id="debug_installation_failures_using_the_setup_api_logs"></span><span id="DEBUG_INSTALLATION_FAILURES_USING_THE_SETUP_API_LOGS"></span>调试使用安装程序 API 日志的安装失败

安装程序 API 日志 （setupapi.app.log 和 setupapi.dev.log） 包含有用的信息来调试记录此测试的驱动程序安装失败。 安装程序 API 日志可以位于 %windir%\\inf\\目录上的测试系统。

若要增加详细级别和潜在有效性这些日志，请重新安装测试之前的以下注册表项设置为 0x2000FFFF:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[设备基础测试](device-fundamentals-tests.md)

[设备基础测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供 WDTF 简单 I/O 插件](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[如何测试在运行时从命令提示符下的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






