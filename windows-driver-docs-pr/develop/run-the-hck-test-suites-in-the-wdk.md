---
ms.assetid: 3FC63BAD-4B95-40AB-BFBE-88A3274B76E8
title: 如何在 WDK 8.1 中运行 HCK 测试套件
description: 为了可以更轻松地在 WDK 中测试 Windows 驱动程序，从 WDK 8.1 起，你可以选择要在测试计算机上运行的 HCK 测试套件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62f841b6a80f0b70827cb669e9cfdd926ccd8d05
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733337"
---
# <a name="how-to-run-the-hck-test-suites-in-wdk-81"></a>如何在 WDK 8.1 中运行 HCK 测试套件

为了可以更轻松地在 WDK 中测试 Windows 驱动程序，从 WDK 8.1 起，你可以选择要在测试计算机上运行的 HCK 测试套件。 [HCK 测试套件](#HCK_test_suites)包括设备基础功能测试以及图形、映像、无线 LAN、移动宽带（CDMA 和 GSM）和 WLAN Direct 设备测试。 这些测试与 Windows 硬件认证工具包 (Windows HCK) 中的测试相同。 有关 Windows HCK 的信息，请参阅 [Windows 硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))。

你可以通过命令提示符窗口或 Visual Studio 运行 HCK 测试。 此外，你可以将这些测试复制到新的位置（其他计算机或 U 盘），然后从该位置运行测试。 自动启动测试将会设置运行测试所需的任何本地配置。

-   [在测试计算机上使用 Visual Studio 运行 HCK 测试套件](#run_hck_from_vs)
-   [通过命令提示符窗口运行 HCK 测试套件](#run_hck_script)

## <a name="span-idrun_hck_from_vsspanspan-idrun_hck_from_vsspanrunning-the-hck-test-suites-on-a-test-computer-using-visual-studio"></a><span id="run_hck_from_vs"></span><span id="RUN_HCK_FROM_VS"></span>在测试计算机上使用 Visual Studio 运行 HCK 测试套件


按照[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md) 中的说明进行操作（如果尚未这样做）。 配置完测试计算机后，测试计算机的名称将显示在工具栏中。 请务必选择为使用 HCK 测试套件进行测试的设备配置的测试计算机。

安装设备和驱动程序以及任何其他测试拓扑要求（请参阅测试设备的 HCK 测试先决条件），视需要准备测试计算机。 你将使用 Visual Studio 和 WDK 8.1 运行测试，而不是 HCK Studio 和 HCK 控制器。

**选择要在测试计算机上运行的 HCK 测试套件**

1.  从“驱动程序”菜单中，选择“测试”，然后选择“测试组资源管理器”。
2.  在“驱动程序测试组资源管理器”窗口中，选择其中一个 [HCK 测试套件](#HCK_test_suites)。

    选择测试套件时，该测试套件将显示在“驱动程序测试组”  窗口中。

3.  请务必选择为使用 HCK 测试套件进行测试的设备配置的测试计算机。
4.  若要使用 HCK 测试套件，你还必须遵循测试设备的配置要求。
5.  你可以使用复选框来选择与目标测试计算机架构（x86、x64、ARM）匹配的测试。
6.  从“驱动程序”菜单中，选择“测试”&gt;“运行测试” 。 默认情况下，“运行”测试命令将运行当前所选测试组中的所有测试。

此外，你还可以复制提供的 HCK 测试套件之一（并将其导出）以及必要的测试支持文件，以便通过命令提示符窗口运行测试套件。

**导出测试套件**

1.  在“测试组资源管理器”中，选择并按住（或右键单击）要复制的 HCK 测试套件，然后选择快捷方式菜单中的“导出测试套件...”。 （此命令将运行 **CopyMe.cmd** 脚本）。
2.  选择测试套件的目标文件夹。 你可以将测试套件导出至网络共享或 U 盘。
3.  若要运行 HCK 测试套件，请在测试计算机上使用提升的权限打开命令提示符窗口。 导航至目标目录并运行 **RunMe.cmd** 脚本。 有关详细信息，请参阅[通过命令提示符窗口运行 HCK 测试套件](#RunMe)。

## <a name="span-idrun_hck_scriptspanspan-idrun_hck_scriptspanrunning-the-hck-test-suites-from-a-command-prompt-window"></a><span id="run_hck_script"></span><span id="RUN_HCK_SCRIPT"></span>通过命令提示符窗口运行 HCK 测试套件


**复制 HCK 测试套件**

1.  打开 Visual Studio 命令提示符窗口。 导航至 %WindowsSdkDir%\\Testing\\Tests\\HCK Tests\\Basic 目录。 例如，C:\\Program Files (x86)\\Windows Kits\\8.1\\Testing\\Tests\\HCK Tests\\Basic
2.  运行 **CopyMe.cmd** 脚本并指定测试套件的名称和目标目录。 此脚本具有以下语法：

    ```cpp
    CopyMe.cmd testSuite destinationPath
    ```

    *testSuite* 为以下值之一：

    -   Device.Device Fundamentals

    -   Device.Graphics

    -   Device.Imaging

    -   Device.Network.MobileBroadband.CDMA

    -   Device.Network.MobileBroadband.GSM

    -   Device.Network.WLAN

    *destinationPath* 可以是任何有效路径，包括 UNC 路径。 例如，你可以将 HCK 测试套件复制到 U 盘或服务器上的共享目录。

    ```cpp
    C:\Program Files (x86)\Windows Kits\8.1\Testing\Tests\HCK Tests\Basic>CopyMe "De
    vice.Device Fundamentals" d:\temp\devfund
    Copying test target setup installers
    Copying TAEF and WDTF infrastructure
    Copying debuggers infrastructure
    Copying x86 tools
    Copying x64 tools
    Copying arm tools
    Copying test suite
    Copy complete!

    Run on any computer using an administrator command prompt in the same folder as
    the RunMe.cmd script.
    "RunMe.cmd <infFileName>"
    ```

<span id="RunMe"></span><span id="runme"></span><span id="RUNME"></span>
**注意**  如果测试计算机运行的是 Windows 7，则你需要在运行 HCK 测试套件之前下载和安装 [Microsoft .NET Framework 4.5](https://go.microsoft.com/fwlink/p/?linkid=317996)。

 

**通过命令提示符窗口运行 HCK 测试套件**

1.  在为测试配置的测试计算机上，使用提升的权限打开命令提示符窗口（**以管理员身份运行**），然后导航至 HCK 测试套件所复制到的位置。

2.  运行 **RunMe.cmd** 脚本并指定 INF 文件的路径和名称。 此脚本具有以下语法：

    ```cpp
    RunMe.cmd infFileName
    ```

    例如：

    ```cpp
    RunMe.cmd myDriver.inf
    ```

    **注意**  Device.Graphics 测试套件并未使用 INF 文件，但是 **RunMe.cmd** 脚本需要 INF 文件。 如有必要，你可以提供替代 INF 文件的名称。

     

## <a name="span-idhck_test_suitesspanspan-idhck_test_suitesspanspan-idhck_test_suitesspanhct-test-suites"></a><span id="HCK_test_suites"></span><span id="hck_test_suites"></span><span id="HCK_TEST_SUITES"></span>HCT 测试套件


-   [HCK Tests.Basic.Device.Device Fundamentals 测试套件](#HCK_devfund)
-   [HCK Tests.Basic.Device.Graphics 测试套件](#HCK_graphics)
-   [HCK Tests.Basic.Device.Imaging 测试套件](#HCK_imaging)
-   [HCK Tests.Basic.Device.Network.MobileBroadband.CDMA 测试套件](#HCK_CDMA)
-   [HCK Tests.Basic.Device.Network.MobileBroadband.GSM 测试套件](#HCK_GSM)
-   [HCK Tests.Basic.Device.Network.WLAN 测试套件](#HCK_WLAN)

有关指定测试参数的信息，请参阅[设备基础功能测试参数](how-to-select-and-configure-the-device-fundamental-tests.md)。 如果进行测试的设备或其子设备之一为 WLAN 适配器或网络设备，则你可能需要设置 *Wpa2PskAesSsid*、*Wpa2PskPassword* 或 *WDTFREMOTESYSTEM* 参数。

### <a name="span-idhck_devfundspanspan-idhck_devfundspanspan-idhck_devfundspanhck-testsbasicdevicedevice-fundamentals-test-suite"></a><span id="HCK_devfund"></span><span id="hck_devfund"></span><span id="HCK_DEVFUND"></span>HCK Tests.Basic.Device.Device Fundamentals 测试套件

使用此套件进行所有设备类型的常规可靠性测试。 你必须遵循 [Device.Fundamentals 可靠性测试先决条件](/previous-versions/windows/hardware/hck/jj191690(v=vs.85))中所述的 HCK 测试的硬件、软件和测试要求。 你将使用 Visual Studio 和 WDK 8.1 运行基本测试，而不是 HCK Studio 和 HCK 控制器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Device Fundamentals 测试套件</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>硬件、软件和测试要求</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309665" data-raw-source="[Device.Fundamentals Reliability Testing Prerequisites](/previous-versions/windows/hardware/hck/jj191690(v=vs.85))">Device.Fundamentals 可靠性测试先决条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>测试描述</strong></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/hck/dn260411(v=vs.85)" data-raw-source="[DF - PNP (disable and enable) with IO Before and After (Basic)](/previous-versions/windows/hardware/hck/dn260411(v=vs.85))">DF - PNP（禁用和启用），带 IO 之前和之后（基本）</a></p>
<p><a href="/previous-versions/windows/hardware/hck/dn247481(v=vs.85)" data-raw-source="[DF - Sleep with IO Before and After (Basic)](/previous-versions/windows/hardware/hck/dn247481(v=vs.85))">DF - 睡眠，带 IO 之前和之后（基本）</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_graphicsspanspan-idhck_graphicsspanspan-idhck_graphicsspanhck-testsbasicdevicegraphics-test-suite"></a><span id="HCK_graphics"></span><span id="hck_graphics"></span><span id="HCK_GRAPHICS"></span>HCK Tests.Basic.Device.Graphics 测试套件

使用此测试套件测试图形适配器或芯片集。 你必须遵循[图形适配器或芯片集测试先决条件](/previous-versions/windows/hardware/hck/hh998923(v=vs.85))中所述的 HCK 测试的硬件、软件和测试要求。 你将使用 Visual Studio 和 WDK 8.1 运行基本测试，而不是 HCK Studio 和 HCK 控制器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Graphics 测试套件</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>硬件、软件和测试要求</strong></td>
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=309671" data-raw-source="[Graphic Adapter or Chipset Testing Prerequisites](/previous-versions/windows/hardware/hck/hh998923(v=vs.85))">图形适配器或芯片集测试先决条件</a></td>
</tr>
<tr class="even">
<td align="left"><strong>测试描述</strong></td>
<td align="left"><a href="/previous-versions/windows/hardware/hck/hh998416(v=vs.85)" data-raw-source="[Graphic Adapter or Chipset Tests](/previous-versions/windows/hardware/hck/hh998416(v=vs.85))">图形适配器或芯片集测试</a></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_imagingspanspan-idhck_imagingspanspan-idhck_imagingspanhck-testsbasicdeviceimaging-test-suite"></a><span id="HCK_imaging"></span><span id="hck_imaging"></span><span id="HCK_IMAGING"></span>HCK Tests.Basic.Device.Imaging 测试套件

使用此测试套件测试打印机。 此测试套件使用 HCK [Device.Imaging 测试](/previous-versions/windows/hardware/hck/jj123724(v=vs.85))中的测试。 你将使用 Visual Studio 和 WDK 8.1 运行基本测试，而不是 HCK Studio 和 HCK 控制器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Imaging 测试套件</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>硬件、软件和测试要求</strong></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/hck/jj124568(v=vs.85)" data-raw-source="[Printer Testing Prerequisites](/previous-versions/windows/hardware/hck/jj124568(v=vs.85))">打印机测试先决条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>测试描述</strong></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/hck/hh998007(v=vs.85)" data-raw-source="[Printer Tests](/previous-versions/windows/hardware/hck/hh998007(v=vs.85))">打印机测试</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_cdmaspanspan-idhck_cdmaspanhck-testsbasicdevicenetworkmobilebroadbandcdma-test-suite"></a><span id="HCK_CDMA"></span><span id="hck_cdma"></span>HCK Tests.Basic.Device.Network.MobileBroadband.CDMA 测试套件

使用此测试套件测试移动宽带 CDMA 设备。 请遵循[移动宽带测试先决条件](/previous-versions/windows/hardware/hck/hh998960(v=vs.85))中所述的设备设置和配置指南。 你将使用 Visual Studio 和 WDK 8.1 运行基本测试，而不是 HCK Studio 和 HCK 控制器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Network.MobileBroadband.CDMA 测试套件</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>硬件、软件和测试要求</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309676" data-raw-source="[Mobile Broadband Testing Prerequisites](/previous-versions/windows/hardware/hck/hh998960(v=vs.85))">移动宽带测试先决条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>测试描述</strong></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/hck/dn293733(v=vs.85)" data-raw-source="[CDMA Tests](/previous-versions/windows/hardware/hck/dn293733(v=vs.85))">CDMA 测试</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_gsmspanspan-idhck_gsmspanhck-testsbasicdevicenetworkmobilebroadbandgsm-test-suite"></a><span id="HCK_GSM"></span><span id="hck_gsm"></span>HCK Tests.Basic.Device.Network.MobileBroadband.GSM 测试套件

使用此测试套件测试移动宽带 GSM 设备。 请遵循[移动宽带测试先决条件](/previous-versions/windows/hardware/hck/hh998960(v=vs.85))中所述的设备设置和配置指南。 你将使用 Visual Studio 和 WDK 8.1 运行基本测试，而不是 HCK Studio 和 HCK 控制器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Network.MobileBroadband.GSM 测试套件</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>硬件、软件和测试要求</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309676" data-raw-source="[Mobile Broadband Testing Prerequisites](/previous-versions/windows/hardware/hck/hh998960(v=vs.85))">移动宽带测试先决条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>测试描述</strong></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/hck/dn247238(v=vs.85)" data-raw-source="[GSM Tests](/previous-versions/windows/hardware/hck/dn247238(v=vs.85))">GSM 测试</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_wlanspanspan-idhck_wlanspanhck-testsbasicdevicenetworkwlan-test-suite"></a><span id="HCK_WLAN"></span><span id="hck_wlan"></span>HCK Tests.Basic.Device.Network.WLAN 测试套件

使用此测试套件测试无线 LAN (802.11) 设备。 请遵循 HCK 的[无线 LAN (802.11) 测试先决条件](/previous-versions/windows/hardware/hck/jj123847(v=vs.85))中所述的设备设置和配置指南。 你将使用 Visual Studio 和 WDK 8.1 运行基本测试，而不是 HCK Studio 和 HCK 控制器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Network.WLAN 测试套件</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>硬件、软件和测试要求</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309679" data-raw-source="[Wireless LAN (802.11) Testing Prerequisites](/previous-versions/windows/hardware/hck/jj123847(v=vs.85))">无线 LAN (802.11) 测试先决条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>测试描述</strong></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/hck/dn247288(v=vs.85)" data-raw-source="[WLAN L1 Tests](/previous-versions/windows/hardware/hck/dn247288(v=vs.85))">WLAN L1 测试</a></p></td>
</tr>
</tbody>
</table>

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

* [如何使用 Visual Studio 测试驱动程序运行时](testing-a-driver-at-runtime.md)
* [如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
* [Windows 调试入门](../debugger/getting-started-with-windows-debugging.md)
* [硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))
* [Windows 硬件认证工具包 (HCK)](/windows-hardware/test/hlk/)
* [如何在运行时通过命令提示符测试驱动程序](how-to-test-a-driver-at-runtime-from-a-command-prompt.md)