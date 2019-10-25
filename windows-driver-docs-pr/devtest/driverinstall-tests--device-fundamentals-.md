---
title: 驱动程序安装测试（设备基础功能）
description: 驱动程序安装测试类别包括多次卸载和重新安装驱动程序以测试安装功能的测试。
ms.assetid: 3FC00D4B-6520-45F1-805C-A5F8B6AACAC8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025f298797753685bc541cd573239bfa9498e3f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840276"
---
# <a name="driver-install-tests-device-fundamentals"></a>驱动程序安装测试（设备基础功能）


驱动程序安装测试类别包括多次卸载和重新安装驱动程序以测试安装功能的测试。 每次重新安装之后，这些测试将启动针对驱动程序和设备的 i/o 测试。 这些测试旨在提高需要安装和重新安装设备驱动程序或设备的最终用户的总体体验。

## <a name="span-iddriverinstall_testsspanspan-iddriverinstall_testsspandriverinstall-tests"></a><span id="driverinstall_tests"></span><span id="DRIVERINSTALL_TESTS"></span>DriverInstall 测试


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
<td align="left"><p><span id="Reinstall_with_IO_Before_and_After"></span><span id="reinstall_with_io_before_and_after"></span><span id="REINSTALL_WITH_IO_BEFORE_AND_AFTER"></span>在之前和之后通过 IO 重新安装</p></td>
<td align="left"><p>此测试将卸载并重新安装所选设备的驱动程序，并在设备上运行 i/o 测试。</p>
<p><strong>测试二进制文件：</strong>Devfund_Reinstall_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong>Reinstall_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idabout_the_reinstall_with_i_o_before_and_after_testspanspan-idabout_the_reinstall_with_i_o_before_and_after_testspanspan-idabout_the_reinstall_with_i_o_before_and_after_testspanabout-the-reinstall-with-io-before-and-after-test"></a><span id="About_the_ReInstall_with_I_O_Before_and_After_test"></span><span id="about_the_reinstall_with_i_o_before_and_after_test"></span><span id="ABOUT_THE_REINSTALL_WITH_I_O_BEFORE_AND_AFTER_TEST"></span>关于测试前后的 i/o 重新安装


此测试执行以下操作：

1.  验证测试设备及其后代是否未报告任何设备问题代码。
2.  使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅[提供的 WDTF 简单 i/o 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)。
3.  使用[**IWDTFDriverSetupAction2：： UpdateDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-updatedriver)方法在测试设备上重新安装原始驱动程序。
4.  验证测试设备及其后代是否未报告任何设备问题代码。
5.  使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅[提供的 WDTF 简单 i/o 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)。
6.  如果步骤 \#3 需要重新启动，则重新启动系统。
7.  在测试设备上使用[**IWDTFDriverSetupAction2：： UnInstallDriverPermanently**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-uninstalldriverpermanently)方法安装 NULL 驱动程序，以便在需要重新启动时重新启动系统。
8.  使用[**IWDTFDriverSetupAction2：： UpdateDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-updatedriver)方法在受测设备上重新安装原始驱动程序。
9.  验证测试设备及其后代是否未报告任何设备问题代码。
10. 使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅[提供的 WDTF 简单 i/o 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)。
11. 多次重复步骤 1-10。

### <a name="span-iddebug_installation_failures_using_the_setup_api_logsspanspan-iddebug_installation_failures_using_the_setup_api_logsspanspan-iddebug_installation_failures_using_the_setup_api_logsspandebug-installation-failures-using-the-setup-api-logs"></a><span id="Debug_installation_failures_using_the_Setup_API_logs"></span><span id="debug_installation_failures_using_the_setup_api_logs"></span><span id="DEBUG_INSTALLATION_FAILURES_USING_THE_SETUP_API_LOGS"></span>使用安装程序 API 日志调试安装失败

安装程序 API 日志（setupapi.log 和 setupapi.log）包含用于调试此测试记录的驱动程序安装失败的有用信息。 可在测试系统上的% windir%\\inf\\ 目录下找到安装程序 API 日志。

若要提高这些日志的详细程度和潜在有用性，请在运行重新安装测试之前，将以下注册表项设置为0x2000FFFF：

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://docs.microsoft.com/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

 

 






