---
title: 睡眠测试（设备基础功能）
description: 设备基础知识睡眠测试运行 I/O 和指定设备上的即插即用操作之前和之后，或在系统睡眠状态转换。
ms.assetid: 38B65078-B436-4C24-B973-032702DB9CBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88c65c9e5df138877d264758003fc0adf2312744
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374409"
---
# <a name="sleep-tests-device-fundamentals"></a>睡眠测试（设备基础功能）


设备基础知识睡眠测试运行 I/O 和指定设备上的即插即用操作之前和之后，或在系统睡眠状态转换。 睡眠测试可确保待测设备允许系统以重复循环的所有受支持的休眠状态。 此外，它可确保通过简单的 I/O 压力测试这些状态更改后该设备仍然正常工作。

## <a name="sleep-tests"></a>进入睡眠状态的测试


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
<td align="left"><p><span id="Critical_Sleep_with_I_O_before_and_after"></span><span id="critical_sleep_with_i_o_before_and_after"></span><span id="CRITICAL_SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>使用之前和之后的 I/O 的关键睡眠</p></td>
<td align="left"><p>该测试在系统上执行关键睡眠状态转换，并在之前的设备上以及每种睡眠状态周期后执行 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_Critical_Sleep_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Sleep_with_I_O_during"></span><span id="critical_sleep_with_i_o_during"></span><span id="CRITICAL_SLEEP_WITH_I_O_DURING"></span>使用期间的 I/O 的关键睡眠</p></td>
<td align="left"><p>该测试在系统上执行关键睡眠状态转换，并在设备上执行 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_Critical_Sleep_With_IO_During.wsc</p>
<p><strong>测试方法：</strong>Critical_Sleep_With_IO_During</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_and_PNP__disable_and_enable__with_I_O_Before_and_After"></span><span id="sleep_and_pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="SLEEP_AND_PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>睡眠和 PNP （禁用和启用） 与 I/O 之前和之后</p></td>
<td align="left"><p>该测试周期系统发起各种睡眠状态，并执行 I/O 和基本 PnP （禁用/启用） 在设备上之前和之后每个睡眠状态周期。</p>
<p>有关详细信息，请参阅<a href="#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test" data-raw-source="[About the Sleep and PNP disable and enable with IO Before and After test](#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test)">有关睡眠和 PNP 禁用和启用 IO 前后的测试和之后</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_Sleep_PNP_DisableEnable_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>Sleep_PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_I_O_Before_and_After"></span><span id="sleep_with_i_o_before_and_after"></span><span id="SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>之前和之后进行的 I/O 睡眠状态</p></td>
<td align="left"><p>此测试周期通过各种睡眠状态的系统，每个睡眠状态循环前后的设备上执行 I/O。</p>
<p>有关详细信息，请参阅<a href="#about-the-sleep-with-io-before-and-after-test" data-raw-source="[About the Sleep with IO Before And After test](#about-the-sleep-with-io-before-and-after-test)">有关睡眠状态与 IO 之前和之后测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_Sleep_With_IO_BeforeAndAfter.wsc</p>
<p><strong>测试方法：</strong>Sleep_With_Io_Before_And_After</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_with_I_O_during"></span><span id="sleep_with_i_o_during"></span><span id="SLEEP_WITH_I_O_DURING"></span>与 I/O 期间进入睡眠状态</p></td>
<td align="left"><p>该测试周期系统发起各种睡眠状态，并在设备上执行 I/O。</p>
<p><strong>测试二进制文件：</strong>Devfund_Sleep_With_IO_During.wsc</p>
<p><strong>测试方法：</strong>Sleep_With_IO_During</p>
<p><strong>参数：</strong> -请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test"></a>有关睡眠和 PNP 禁用和启用 IO 前后的测试和之后


此测试将执行以下操作：

1.  验证测试设备及其子代未报告任何设备问题代码。
2.  在测试设备和使用 WDTF 简单 I/O 插件及其后代上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)有关详细信息。
3.  将测试系统发送到其第一种受支持的休眠状态并继续从一段时间后睡眠状态系统。
4.  验证测试设备及其子代未报告任何设备问题代码。
5.  在测试设备和使用 WDTF 简单 I/O 插件及其后代上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)有关详细信息。
6.  如果测试设备是可以为禁用状态，测试禁用和启用使用 WDTF 即插即用操作接口，对测试设备，请参阅[ **IWDTFPNPAction2::DisableDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice)并[ **IWDTFPNPAction2::EnableDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice)方法的详细信息。
7.  验证测试设备及其子代未报告任何设备问题代码。
8.  在测试设备和使用 WDTF 简单 I/O 插件及其后代上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)有关详细信息。
9.  重复步骤 3-8，每个受支持测试系统睡眠的状态。
10. 重复步骤 1-9 几次。

## <a name="about-the-sleep-with-io-before-and-after-test"></a>有关与 IO 之前和之后测试睡眠


此测试将执行以下操作：

1.  验证 reporting 设备问题代码在系统上没有任何设备。
2.  使用 WDTF 简单 I/O 插件在系统上每个设备上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)有关详细信息。
3.  将测试系统发送到其第一种受支持的休眠状态并继续从一段时间后睡眠状态系统。
4.  验证 reporting 设备问题代码在系统上没有任何设备。
5.  使用 WDTF 简单 I/O 插件在系统上每个设备上测试 I/O。 请参阅[提供 WDTF 简单 I/O 插件](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)有关详细信息。
6.  对于每个受支持的休眠状态的测试系统重复步骤 3-5。
7.  重复步骤 1-6 几次。

## <a name="related-topics"></a>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](https://docs.microsoft.com/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

 

 






