---
title: 睡眠测试（设备基础功能）
description: 设备基础睡眠测试在指定的设备上、之前和之后或在系统睡眠状态转换期间运行 i/o 和 PnP 操作。
ms.assetid: 38B65078-B436-4C24-B973-032702DB9CBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de217170bd9db9d0c23db372ad085a91d7a56176
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384035"
---
# <a name="sleep-tests-device-fundamentals"></a>睡眠测试（设备基础功能）


设备基础睡眠测试在指定的设备上、之前和之后或在系统睡眠状态转换期间运行 i/o 和 PnP 操作。 睡眠测试可确保所测试的设备能够通过所有受支持的睡眠状态进行循环。 此外，它还可以确保在这些状态发生更改后，设备仍能正常运行，这是因为简单的 i/o 压力测试。

## <a name="sleep-tests"></a>睡眠测试


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">测试</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Critical_Sleep_with_I_O_before_and_after"></span><span id="critical_sleep_with_i_o_before_and_after"></span><span id="CRITICAL_SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>前后 i/o 的关键睡眠</p></td>
<td align="left"><p>此测试执行系统上的关键睡眠状态转换，并对每个睡眠状态周期前后的设备执行 i/o。</p>
<p><strong>测试二进制文件：</strong> Devfund_Critical_Sleep_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong> Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Sleep_with_I_O_during"></span><span id="critical_sleep_with_i_o_during"></span><span id="CRITICAL_SLEEP_WITH_I_O_DURING"></span>期间 i/o 严重睡眠</p></td>
<td align="left"><p>此测试执行系统上的关键睡眠状态转换，并在设备上执行 i/o。</p>
<p><strong>测试二进制文件：</strong> Devfund_Critical_Sleep_With_IO_During. wsc</p>
<p><strong>测试方法：</strong> Critical_Sleep_With_IO_During</p>
<p><strong>参数：</strong> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_and_PNP__disable_and_enable__with_I_O_Before_and_After"></span><span id="sleep_and_pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="SLEEP_AND_PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>睡眠和 PNP (在之前和之后使用 i/o 禁用和启用) </p></td>
<td align="left"><p>此测试通过各种睡眠状态循环系统，并对每个睡眠状态周期前后的设备执行 i/o 和基本 PnP (禁用/启用) 。</p>
<p>有关详细信息，请参阅 <a href="#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test" data-raw-source="[About the Sleep and PNP disable and enable with IO Before and After test](#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test)">关于睡眠和 PNP 在测试前后使用 IO 禁用和启用</a>。</p>
<p><strong>测试二进制文件：</strong> Devfund_Sleep_PNP_DisableEnable_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong> Sleep_PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>参数：</strong> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_I_O_Before_and_After"></span><span id="sleep_with_i_o_before_and_after"></span><span id="SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>在前后 i/o</p></td>
<td align="left"><p>此测试通过各种睡眠状态循环系统，并在每个睡眠状态周期前后在设备上执行 i/o。</p>
<p>有关详细信息，请参阅 <a href="#about-the-sleep-with-io-before-and-after-test" data-raw-source="[About the Sleep with IO Before And After test](#about-the-sleep-with-io-before-and-after-test)">关于测试前后 IO 的睡眠</a>。</p>
<p><strong>测试二进制文件：</strong> Devfund_Sleep_With_IO_BeforeAndAfter. wsc</p>
<p><strong>测试方法：</strong> Sleep_With_Io_Before_And_After</p>
<p><strong>参数：</strong> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_with_I_O_during"></span><span id="sleep_with_i_o_during"></span><span id="SLEEP_WITH_I_O_DURING"></span>在期间休眠 i/o</p></td>
<td align="left"><p>此测试通过各种睡眠状态循环系统，并在设备上执行 i/o。</p>
<p><strong>测试二进制文件：</strong> Devfund_Sleep_With_IO_During. wsc</p>
<p><strong>测试方法：</strong> Sleep_With_IO_During</p>
<p><strong>参数：</strong> - 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test"></a>关于睡眠和 PNP 在测试前后使用 IO 禁用和启用


此测试执行以下操作：

1.  验证测试设备及其后代是否未报告任何设备问题代码。
2.  使用 WDTF 简单 i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
3.  将测试系统发送到其第一个受支持的睡眠状态，然后在一段时间后从睡眠状态恢复系统。
4.  验证测试设备及其后代是否未报告任何设备问题代码。
5.  使用 WDTF 简单 i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
6.  如果可以禁用测试设备，则测试将使用 WDTF PnP 操作接口禁用和启用测试设备，有关详细信息，请参阅 [**IWDTFPNPAction2：:D isabledevice**](/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice) 和 [**IWDTFPNPAction2：： EnableDevice**](/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice) 方法。
7.  验证测试设备及其后代是否未报告任何设备问题代码。
8.  使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
9.  对于每个受支持的测试系统睡眠状态，重复步骤3-8。
10. 多次重复步骤1-9。

## <a name="about-the-sleep-with-io-before-and-after-test"></a>关于测试前后 IO 的睡眠


此测试执行以下操作：

1.  验证系统报告设备问题代码上是否没有设备。
2.  使用 WDTF 简单 i/o 插件测试系统上每台设备上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
3.  将测试系统发送到其第一个受支持的睡眠状态，然后在一段时间后从睡眠状态恢复系统。
4.  验证系统报告设备问题代码上是否没有设备。
5.  使用 WDTF 简单 i/o 插件测试系统上每台设备上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
6.  对于每个受支持的测试系统睡眠状态，重复步骤 3-5。
7.  多次重复步骤 1-6。

## <a name="related-topics"></a>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](../wdtf/provided-wdtf-simpleio-plug-ins.md)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](/windows-hardware/drivers)

 

