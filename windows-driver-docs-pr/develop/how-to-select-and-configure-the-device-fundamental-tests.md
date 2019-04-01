---
ms.assetid: DDAF6D33-46D8-4A04-A3DC-C9FE26ABD003
title: 如何选择和配置设备基础功能测试
description: 适用于 Windows 8 的 WDK 提供了一个驱动程序测试框架，其中包括一组设备基础功能测试。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20842ec8fd3dd48672fe9ea1f7301739c36d00aa
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349144"
---
# <a name="how-to-select-and-configure-the-device-fundamentals-tests"></a>如何选择和配置设备基础功能测试

适用于 Windows 8 的 WDK 提供了一个驱动程序测试框架，其中包括一组设备基础功能测试。 设备基础功能测试是在 Microsoft 内部用于测试 Windows 和 WDK 随附的驱动程序和驱动程序样本以及在外部作为 [Windows 硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=8705)一部分的一系列测试。 可以在开发环境中运行测试。 运行测试时，可以使用与 Windows 认证测试所使用的相同参数，或者可以根据测试和调试需要配置和自定义运行时参数。

## <a name="span-idgettingthemostfromthedevicefundamentalstestsspanspan-idgettingthemostfromthedevicefundamentalstestsspanspan-idgettingthemostfromthedevicefundamentalstestsspangetting-the-most-from-the-device-fundamentals-tests"></a><span id="Getting_the_most_from_the_Device_Fundamentals_tests"></span><span id="getting_the_most_from_the_device_fundamentals_tests"></span><span id="GETTING_THE_MOST_FROM_THE_DEVICE_FUNDAMENTALS_TESTS"></span>充分利用设备基础功能测试


若要充分利用设备基础功能测试，设备必须受默认的 I/O 插件支持。若要了解设备类型是否受支持以及确定是否有特定的测试要求，请参阅 [Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/Library/Windows/Hardware/Hh781398)（提供的 WDTF 简单 I/O 插件）。设备基础功能测试还包括一个实用程序，可以用其测试设备是否受支持。 如果设备不受支持，则可以在 Visual Studio 中 创建一个 WDTF 简单 I/O 插件。 有关详细信息，请参阅 [How to customize I/O for your device using the WDTF Simple I/O Action Plug-in](https://msdn.microsoft.com/Library/Windows/Hardware/Hh706277)（如何使用 WDTF 简单 I/O 操作插件为你的设备自定义 I/O）。

## <a name="span-idaboutthedevicefundamentalstestsspanspan-idaboutthedevicefundamentalstestsspanspan-idaboutthedevicefundamentalstestsspanabout-the-device-fundamentals-tests"></a><span id="About_the_Device_Fundamentals_Tests"></span><span id="about_the_device_fundamentals_tests"></span><span id="ABOUT_THE_DEVICE_FUNDAMENTALS_TESTS"></span>关于设备基础功能测试


WDK 提供有两种配置的设备基础功能测试：基本和认证。 在两种配置下，都可以通过编辑测试参数来调整测试长度、要执行的测试周期数以及其他测试参数，具体取决于需要测试的目标设备或驱动程序。 基本配置适用于通用驱动程序和设备的测试和调试。 在开发周期早期及整个过程中均可使用基本配置。 基本配置下的测试所使用的设置与 Windows 认证测试使用的设置相同，但前者的运行时更短。 在认证配置下，测试使用的设置与 Windows 认证测试使用的设置完全相同。 使用认证配置来验证设备或驱动程序是否做好 [Windows 硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=8705)的准备。

[设备基础功能测试](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)包括以下类别的测试。

-   [混沌测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673008)
-   [覆盖范围测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673009)
-   [CPU 压力测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673010)
-   [驱动程序安装测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673012)
-   [I/O 测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673013)
-   [渗透压力测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673014)
-   [PNP 测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673015)
-   [重新启动测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673016)
-   [睡眠测试（设备基础功能）](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673017)
-   [实用程序](#utility_tests)
-   [驱动程序验证程序](#utility_tests)

### <a name="span-idsettingtherun-timetestparametersspanspan-idsettingtherun-timetestparametersspanspan-idsettingtherun-timetestparametersspansetting-the-run-time-test-parameters"></a><span id="Setting_the_run-time_test_parameters"></span><span id="setting_the_run-time_test_parameters"></span><span id="SETTING_THE_RUN-TIME_TEST_PARAMETERS"></span>设置运行时测试参数

可以编辑多个设备基础功能测试的运行时参数。 在“驱动程序测试组”窗口中，测试名称旁边的箭头 (») 指示你可以更改此测试参数。 单击箭头 (») 即可显示运行时参数。

其中一个最常用的参数是 *DQ*，用于指定要测试的目标设备。 默认值 (**IsDevice**) 将测试目标计算机上的所有设备。 *DQ* 参数将通过 [**WDTF**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547) [SDEL](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539571) 查询来确定目标设备。 可以指定特定测试设备，如：

**DeviceID=’USB\\ROOT\_HUB\\4&1CD5D022&0’** 仅选择具有指定 **DeviceID** 的测试设备。

有关 *DQ* 及其他运行时参数的详细信息，请参阅[设备基础功能测试参数](#DevFund_Params)。

## <a name="span-iddevfundparamsspanspan-iddevfundparamsspanspan-iddevfundparamsspandevice-fundamentals-test-parameters"></a><span id="DevFund_Params"></span><span id="devfund_params"></span><span id="DEVFUND_PARAMS"></span>设备基础功能测试参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="DQ"></span><span id="dq"></span><em>DQ</em></p></td>
<td align="left"><p>确定应当用于测试的设备。 <em>DQ</em> 参数将通过 <a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547" data-raw-source="[&lt;strong&gt;WDTF&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547)"><strong>WDTF</strong></a><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff539571" data-raw-source="[SDEL](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539571)">SDEL</a> 查询来确定目标设备。 此查询非常灵活，可用于表示任何数量的设备，从单个设备到系统中的所有设备。</p>
<p>常见示例：</p>
<p></p>
<dl>
<dt><span id="To_test_all_devices_that_were_installed_with_a_specific_INF_File_"></span><span id="to_test_all_devices_that_were_installed_with_a_specific_inf_file_"></span><span id="TO_TEST_ALL_DEVICES_THAT_WERE_INSTALLED_WITH_A_SPECIFIC_INF_FILE_"></span>若要测试安装有特定 INF 文件的所有设备：</dt>
<dd><p><strong>INF::FileName=</strong><em>INF_File_Name</em></p>
<p>例如，<strong>INF::OriginalInfFileName='%InfFileName%'</strong></p>
<p>这是默认值。</p>
</dd>
<dt><span id="To_test_a_device_with_a_specific_Device_Id__"></span><span id="to_test_a_device_with_a_specific_device_id__"></span><span id="TO_TEST_A_DEVICE_WITH_A_SPECIFIC_DEVICE_ID__"></span>若要测试具有特定设备 ID 的设备：</dt>
<dd><p><strong>DeviceId=’</strong><em>DeviceId</em><strong>’</strong></p>
<p>例如，<strong>DeviceID=’USB\ROOT_HUB\4&amp;1CD5D022&amp;0’</strong></p>
</dd>
<dt><span id="_To_test_a_device_with_a_specific_interface_"></span><span id="_to_test_a_device_with_a_specific_interface_"></span><span id="_TO_TEST_A_DEVICE_WITH_A_SPECIFIC_INTERFACE_"></span> 若要测试具有特定接口的设备：</dt>
<dd><p><strong>Interfaces::</strong><em>InterfaceGUID</em></p>
</dd>
<dt><span id="To_test_a_device_with_a_specific_driver_letter_"></span><span id="to_test_a_device_with_a_specific_driver_letter_"></span><span id="TO_TEST_A_DEVICE_WITH_A_SPECIFIC_DRIVER_LETTER_"></span>若要测试具有特定驱动器号的设备：</dt>
<dd><p><strong>Volume::DriverLetter=’</strong><em>DriveLetter</em><strong>’</strong></p>
<p>例如，<strong>Volume::DriverLetter=’c:\’</strong></p>
</dd>
<dt><span id="To_test_a_device_with_a_specific_driver____"></span><span id="to_test_a_device_with_a_specific_driver____"></span><span id="TO_TEST_A_DEVICE_WITH_A_SPECIFIC_DRIVER____"></span>若要测试具有特定驱动程序的设备：</dt>
<dd><p><strong>DriverBinaryNames=</strong><em>mydriver.sys</em></p>
</dd>
<dt><span id="____To_test_all_device_of_a_specific_device_Class___________________"></span><span id="____to_test_all_device_of_a_specific_device_class___________________"></span><span id="____TO_TEST_ALL_DEVICE_OF_A_SPECIFIC_DEVICE_CLASS___________________"></span> 若要测试特定设备类的所有设备：</dt>
<dd><p>例如，<strong>Class=CDROM</strong> 将测试类为 CDROM 的所有设备。</p>
<p>例如，<strong>ClassGUID= {36fc9e60-c465-11cf-8056-444553540000}</strong> 将测试类 GUID 与指定 GUID 匹配的所有设备。 在本示例中，GUID 为 USB 类。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DoPoolCheck"></span><span id="dopoolcheck"></span><span id="DOPOOLCHECK"></span><em>DoPoolCheck</em></p></td>
<td align="left"><p>True 或 False。 通过使用池标记和旁视列表监控驱动程序对分页和非分页系统内存池的使用情况。 此选项还可监控已处理的异常数量变化，这可能指示在异常处理时出错。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ChangeBufferProtectionFlags"></span><span id="changebufferprotectionflags"></span><span id="CHANGEBUFFERPROTECTIONFLAGS"></span><em>ChangeBufferProtectionFlags</em></p></td>
<td align="left"><p>True 或 False。 更改传递至已测试设备的缓冲区的内存保护标志。 此内存保护标志在无访问权限、只读和具有页防护的只读之间变化。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DoSimpleIO"></span><span id="dosimpleio"></span><span id="DOSIMPLEIO"></span><em>DoSimpleIO</em></p></td>
<td align="left"><p>True 或 False。 在执行 PNP 操作之前和之后，在测试设备上运行简单 I/O（如发现）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="DoConcurrentIO"></span><span id="doconcurrentio"></span><span id="DOCONCURRENTIO"></span><em>DoConcurrentIO</em></p></td>
<td align="left"><p>True 或 False。 执行 PnP 操作时，使用 <a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547" data-raw-source="[WDTF](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547)">WDTF</a> 并发 I/O 接口向目标设备堆栈发送 I/O 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="FillZeroPageWithNull"></span><span id="fillzeropagewithnull"></span><span id="FILLZEROPAGEWITHNULL"></span><em>FillZeroPageWithNull</em></p></td>
<td align="left"><p>True 或 False。 映射零页并使用 NULL 值进行填充。 此测试用于确定在取消调用指针之前无法验证指针的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="FuzzTestPeriod"></span><span id="fuzztestperiod"></span><span id="FUZZTESTPERIOD"></span><em>FuzzTestPeriod</em></p></td>
<td align="left"><p>模糊测试周期（分钟）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="HPU"></span><span id="hpu"></span><em>HPU</em></p></td>
<td align="left"><p>指定高处理器使用率百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Impersonate"></span><span id="impersonate"></span><span id="IMPERSONATE"></span><em>Impersonate</em></p></td>
<td align="left"><p>True 或 False。 以用户身份（无管理员权限）运行测试。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="IOPeriod"></span><span id="ioperiod"></span><span id="IOPERIOD"></span><em>IOPeriod</em></p></td>
<td align="left"><p>指定 I/O 周期（分钟）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="IOType"></span><span id="iotype"></span><span id="IOTYPE"></span><em>IOType</em></p></td>
<td align="left"><p>指定 I/O 压力测试的类型：SimpleIOStressEx 或 SimpleIOStressProc（单独进程中的 I/O）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="LPU"></span><span id="lpu"></span><em>LPU</em></p></td>
<td align="left"><p>指定低处理器使用率百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxInBuffer"></span><span id="maxinbuffer"></span><span id="MAXINBUFFER"></span><em>MaxInBuffer</em></p></td>
<td align="left"><p>指定测试传递至 FSCTL（或 IOCTL，对于 IOCTL 测试）中的驱动程序的输入缓冲区最大大小（字节）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinInBuffer"></span><span id="mininbuffer"></span><span id="MININBUFFER"></span><em>MinInBuffer</em></p></td>
<td align="left"><p>指定测试传递至 FSCTL（或 IOCTL，对于 IOCTL 测试）中的驱动程序的输入缓冲区最小大小（字节）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxOutBuffer"></span><span id="maxoutbuffer"></span><span id="MAXOUTBUFFER"></span><em>MaxOutBuffer</em></p></td>
<td align="left"><p>指定测试传递至 FSCTL（或 IOCTL，对于 IOCTL 测试）中的驱动程序的输出缓冲区最大大小（字节）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinOutBuffer"></span><span id="minoutbuffer"></span><span id="MINOUTBUFFER"></span><em>MinOutBuffer</em></p></td>
<td align="left"><p>指定测试传递至 FSCTL（或 IOCTL，对于 IOCTL 测试）中的驱动程序的输出缓冲区最小大小（字节）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxRandomCalls"></span><span id="maxrandomcalls"></span><span id="MAXRANDOMCALLS"></span><em>MaxRandomCalls</em></p></td>
<td align="left"><p>指定测试发出的最大调用次数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MaxTailoredCalls"></span><span id="maxtailoredcalls"></span><span id="MAXTAILOREDCALLS"></span><em>MaxTailoredCalls</em></p></td>
<td align="left"><p>指定在定制的随机测试中测试发出的最大调用次数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxDeviceType"></span><span id="maxdevicetype"></span><span id="MAXDEVICETYPE"></span><em>MaxDeviceType</em></p></td>
<td align="left"><p>指定 FSCTL（或 IOCTL，对于 IOCTL 测试）中的 DeviceType 字段的最大值。 可能的最大值是 65535。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinDeviceType"></span><span id="mindevicetype"></span><span id="MINDEVICETYPE"></span><em>MinDeviceType</em></p></td>
<td align="left"><p>指定 FSCTL（或 IOCTL，对于 IOCTL 测试）中的 DeviceType 字段的最小值。 可能的最小值为 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxFunctionCode"></span><span id="maxfunctioncode"></span><span id="MAXFUNCTIONCODE"></span><em>MaxFunctionCode</em></p></td>
<td align="left"><p>指定 FSCTL（或 IOCTL，对于 IOCTL 测试）中的 FunctionCode 字段的最大值。 可能的最大值是 4095。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinFunctionCode"></span><span id="minfunctioncode"></span><span id="MINFUNCTIONCODE"></span><em>MinFunctionCode</em></p></td>
<td align="left"><p>指定 FSCTL（或 IOCTL，对于 IOCTL 测试）中的 FunctionCode 字段的最小值。 可能的最小值为 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PU"></span><span id="pu"></span><em>PU</em></p></td>
<td align="left"><p>指定处理器使用率百分比</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PingPongPeriod"></span><span id="pingpongperiod"></span><span id="PINGPONGPERIOD"></span><em>PingPongPeriod</em></p></td>
<td align="left"><p>指定乒乓周期（分钟）；它是指处理器在高 (HPU) 和低 (LPU) 处理器使用率水平之间变化的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ResumeDelay"></span><span id="resumedelay"></span><span id="RESUMEDELAY"></span><em>ResumeDelay</em></p></td>
<td align="left"><p>计算机从睡眠模式恢复之后与下一个 I/O 周期开始之前的延迟时间（秒）。 此延迟时间对于让设备恢复其工作状态（续订网络卡的 IP 地址等）来说是必要的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="TestCycles"></span><span id="testcycles"></span><span id="TESTCYCLES"></span><em>TestCycles</em></p></td>
<td align="left"><p>指定要执行的测试周期数（迭代数）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="WDTFREMOTESYSTEM"></span><span id="wdtfremotesystem"></span><em>WDTFREMOTESYSTEM</em></p></td>
<td align="left"><p>仅当进行测试的设备或其子设备之一为没有 IPv6 网关地址的有线网络适配器时才需要使用此参数。 如果网络需要使用此参数，则必须提供一个测试网络适配器可用其连接至测试网络的 IPv6 地址。</p>
<p>示例：<strong>fe80::78b6:810:9c12:46cd</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Wpa2PskAesSsid"></span><span id="wpa2pskaesssid"></span><span id="WPA2PSKAESSSID"></span><em>Wpa2PskAesSsid</em></p></td>
<td align="left"><p>仅当进行测试的设备或其子设备之一为 WLAN 适配器时才需要使用此参数。 提供测试可用其测试 WLAN 适配器的 WPA2 AES WLAN 网络 SSID。</p>
<p>默认值：<strong>kitstestssid</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Wpa2PskPassword"></span><span id="wpa2pskpassword"></span><span id="WPA2PSKPASSWORD"></span><em>Wpa2PskPassword</em></p></td>
<td align="left"><p>仅当进行测试的设备或其子设备之一为 WLAN 适配器时才需要使用此参数。 提供由使用 Wpa2PskAesSsid 参数指定的 WPA2 AES WLAN 网络的密码。</p>
<p>默认值：<strong>password</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idutilitytestsspanspan-idutilitytestsspanutility-tests"></a><span id="utility_tests"></span><span id="UTILITY_TESTS"></span>实用程序测试


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
<td align="left"><p><span id="Display_devices_that_have_WDTF_Simple_I_O_plug-ins"></span><span id="display_devices_that_have_wdtf_simple_i_o_plug-ins"></span><span id="DISPLAY_DEVICES_THAT_HAVE_WDTF_SIMPLE_I_O_PLUG-INS"></span>显示具有 WDTF 简单 I/O 插件的设备</p></td>
<td align="left"><p><strong>参数：</strong>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_devices_that_have_Driver_Verifier_enabled"></span><span id="display_devices_that_have_driver_verifier_enabled"></span><span id="DISPLAY_DEVICES_THAT_HAVE_DRIVER_VERIFIER_ENABLED"></span>显示已启用驱动程序验证程序的设备</p></td>
<td align="left"><p><strong>参数：</strong>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Display_devices"></span><span id="display_devices"></span><span id="DISPLAY_DEVICES"></span>显示设备</p></td>
<td align="left"><p><strong>参数：</strong>无</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddvrftestsspanspan-iddvrftestsspandriver-verifier"></a><span id="dvrf_tests"></span><span id="DVRF_TESTS"></span>驱动程序验证程序


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
<td align="left"><p><span id="Disable_Driver_Verifier"></span><span id="disable_driver_verifier"></span><span id="DISABLE_DRIVER_VERIFIER"></span>禁用驱动程序验证程序</p></td>
<td align="left"><p>禁用测试计算机上的<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)">驱动程序验证程序</a>。</p>
<p><strong>参数：</strong>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Driver_Verifier"></span><span id="enable_driver_verifier"></span><span id="ENABLE_DRIVER_VERIFIER"></span>启用驱动程序验证程序</p></td>
<td align="left"><p>可以使用此测试在测试计算机上为设备的所有驱动程序启用<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)">驱动程序验证程序</a>。</p>
<p><strong>参数：</strong>-请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545470" data-raw-source="[Driver Verifier Options](https://msdn.microsoft.com/library/windows/hardware/ff545470)">驱动程序验证程序选项</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [如何在运行时使用 Visual Studio 测试驱动程序](testing-a-driver-at-runtime.md)
* [设备基础功能测试](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)
* [Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/Library/Windows/Hardware/Hh781398)（提供的 WDTF 简单 I/O 插件）
* [How to customize I/O for your device using the WDTF Simple I/O Action Plug-in](https://msdn.microsoft.com/Library/Windows/Hardware/Hh706277)（如何使用 WDTF 简单 I/O 操作插件为设备自定义 I/O）
 

 






