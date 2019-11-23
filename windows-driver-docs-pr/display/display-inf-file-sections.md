---
title: 显示 INF 文件节
description: 显示 INF 文件节
ms.assetid: 2075a10f-a504-4bdc-8112-9c583c5084bb
keywords:
- sideband 处理 WDK Windows 2000 显示器
- AGP 传输速率 WDK Windows 2000 显示
- SoftwareSettings 部分
- CapabilityOverride
- INF 文件 WDK Windows 2000 显示
- 显示 INF 文件部分 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f22d7938de2acbe4181a5e9e4bc949f62713be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839741"
---
# <a name="display-inf-file-sections"></a>显示 INF 文件节


## <span id="ddk_display_inf_file_sections_gg"></span><span id="DDK_DISPLAY_INF_FILE_SECTIONS_GG"></span>


本部分说明如何编写专门适用于图形适配器安装的安装信息文件（INF）部分。 有关 INF 文件的更多常规信息，请参阅[Inf 文件部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。

### <a name="span-idddinstallsoftwaresettings_sectionspanspan-idddinstallsoftwaresettings_sectionspanspan-idddinstallsoftwaresettings_sectionspanddinstallsoftwaresettings-section"></a><span id="DDInstall.SoftwareSettings_Section"></span><span id="ddinstall.softwaresettings_section"></span><span id="DDINSTALL.SOFTWARESETTINGS_SECTION"></span>DDInstall. SoftwareSettings 部分

*DDInstall*。**SoftwareSettings**节包含[**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)指令和/或[**DelReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)指令。 每个指令指向单独的、写入器定义的 INF 部分，其中包含要添加或删除的安装程序的注册表项。

例如，下面的代码显示一个**AddReg**指令，该指令指向名为**ACME-1234\_SoftwareDeviceSettings**的编写器定义的外接注册表部分。 **DelReg**指令指向名为**ACME-1234\_DeleteSWSettings**的 delete 注册表部分。

```inf
[ACME-1234.SoftwareSettings]
AddReg=ACME-1234_SoftwareDeviceSettings
DelReg=ACME-1234_DeleteSWSettings
```

"添加注册表" 部分会向注册表中添加四个项并设置它们的值，如下面的代码所示。

```inf
[ACME-1234_SoftwareDeviceSettings]
HKR,, InstalledDisplayDrivers, %REG_MULTI_SZ%, Acme1
HKR,, OverRideMonitorPower, %REG_DWORD%, 0
HKR,, MultiFunctionSupported, %REG_DWORD%, 1
HKR,, VideoDebugLevel, %REG_DWORD%, 2
```

前面的代码首先将**InstalledDisplayDrivers**条目的值设置为显示驱动程序的名称。 然后，该代码将**OverRideMonitorPower**条目的值设置为0（换言之， **FALSE**）。 此项只应由 OEM 系统供应商使用，控制监视设备的电源行为（例如，LCD、CRT 或电视）。 设置为1时， **OverRideMonitorPower**会将监视设备的可能电源状态限制为 D0 和 D3。

第三，代码会将**MultiFunctionSupported**条目的值设置为1（换言之，为**TRUE**），这是支持多个 PCI 函数的适配器所需的值。 最后，该代码设置**VideoDebugLevel**项的值，该条目控制检查生成用于调试消息的全局调试级别。 此值的范围为0（无调试消息）到3（最详细的消息）。 有关全局调试级别的详细信息，请参阅[**VideoDebugPrint**](https://docs.microsoft.com/previous-versions/ff570170(v=vs.85))。

大多数视频微型端口驱动程序与 VGA 兼容，且在注册表中不需要**VgaCompatible**项。 如果视频微型端口驱动程序与 VGA 兼容，请将**VgaCompatible**条目添加到注册表中，并在 "添加注册表" 部分将其值设置为1（**TRUE**），如下所示：

```registry
[ACME-1234_SoftwareDeviceSettings]
HKR,, VgaCompatible, %REG_DWORD%, 1
```

有关与 VGA 兼容的视频微型端口驱动程序的详细信息，请参阅[Vga 兼容的视频微型端口驱动程序（Windows 2000 型号）](vga-compatible-video-miniport-drivers--windows-2000-model-.md)。

以下 delete 注册表部分删除三个注册表项： **GraphicsClocking**、 **MemClocking**和**CapabilityOverride**。

```inf
[ACME-1234_DeleteSWSettings]
HKR,, GraphicsClocking
HKR,, MemClocking
HKR,, CapabilityOverride
```

**CapabilityOverride**项指定显示器驱动程序的系统关闭功能。 例如，即使显示驱动程序实现了[**DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)函数，如果在**CapabilityOverride**项中设置了0x10 标志，则无法使用该功能。

**CapabilityOverride**注册表项的值是下表中列出的一个或多个标志的按位 "或"。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>禁用所有硬件加速。 等效于将硬件加速滑动条（在 "控制面板" 的 "<strong>显示</strong>项" 中）移动到最小设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>禁用对 Microsoft DirectDraw 和 Microsoft Direct3D 硬件加速的所有支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>禁用对 Direct3D 硬件加速的所有支持。 阻止对<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"><strong>DdGetDriverInfo</strong></a>的调用<em>，</em>该调用请求从连接到驱动程序的 Direct3D 功能和回调信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>禁用对 OpenGL 可安装客户端驱动程序（ICD）和 miniclient driver （MCD）的所有支持。 阻止对<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)"><strong>DrvSetPixelFormat</strong></a>、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)"><strong>DrvDescribePixelFormat</strong></a>和<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers)"><strong>DrvSwapBuffers</strong></a>的调用到达驱动程序。 还禁止 OPENGL_GETINFO、OPENGL_CMD 和 MCDFUNCS 的转义到达驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>禁用对驱动程序中所有转义的支持。 阻止对<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a>和<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)"><strong>DrvDrawEscape</strong></a>的调用到达驱动程序。</p></td>
</tr>
</tbody>
</table>

 

对于随 Windows 提供的显示驱动程序， **CapabilityOverride**通常设置为0x8，这将禁用 OpenGL。 请注意，不需要设置0x10 标志来禁用 OpenGL，除非要禁用所有转义，否则不应设置0x10 标志。

更新显示驱动程序时，Microsoft Windows XP 和更早版本的操作系统不会删除**CapabilityOverride**注册表项，例如，从随 Windows 提供的驱动程序到独立硬件供应商（IHV）提供的最新驱动程序。 永久性**CapabilityOverride**条目禁用在旧驱动程序中禁用的更新驱动程序中的相同功能。 因此，对于 Windows XP 和更早版本，请在 INF 文件中包含显式删除现有**CapabilityOverride**条目的**DelReg**指令。 更新驱动程序时，Windows XP SP1 和更高版本的操作系统会自动删除**CapabilityOverride**条目，因此，在这些系统中，无需删除**CapabilityOverride**条目。

### <a name="span-iddisabling_agp_transfer_rates_and_sideband_addressingspanspan-iddisabling_agp_transfer_rates_and_sideband_addressingspanspan-iddisabling_agp_transfer_rates_and_sideband_addressingspandisabling-agp-transfer-rates-and-sideband-addressing"></a><span id="Disabling_AGP_Transfer_Rates_and_Sideband_Addressing"></span><span id="disabling_agp_transfer_rates_and_sideband_addressing"></span><span id="DISABLING_AGP_TRANSFER_RATES_AND_SIDEBAND_ADDRESSING"></span>禁用 AGP 传输速率和 Sideband 寻址

如有必要，可以修改显示适配器的 INF 文件，以禁用特定的 AGP 传输速率或 sideband 寻址。 请注意，微型端口驱动程序可以在调用[**AgpSetRate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_set_rate)时更改 AGP 传输速率，但不允许此类调用更改 INF 文件中禁用的传输速率。

Windows 驱动程序工具包（WDK）附带的*regstr*头文件定义了以下一组标志。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_1X_RATE</p></td>
<td align="left"><p>0x00000001L</p></td>
<td align="left"><p>禁用单速率（66 MHz）传输速率。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_2X_RATE</p></td>
<td align="left"><p>0x00000002L</p></td>
<td align="left"><p>禁用单速率传输速率的两倍。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_4X_RATE</p></td>
<td align="left"><p>0x00000004L</p></td>
<td align="left"><p>禁用单速率传输速率的四倍。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_8X_RATE</p></td>
<td align="left"><p>0x00000008L</p></td>
<td align="left"><p>禁用单速率传输速率的8倍。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_SBA_ENABLE</p></td>
<td align="left"><p>0x00000100L</p></td>
<td align="left"><p>禁用 sideband 寻址（SBA）。</p></td>
</tr>
</tbody>
</table>

 

存在两种类型的设置：全局设置和特定于平台的设置。 注册表包含位于以下位置的全局条目：

```registry
HKLM,"SYSTEM\CurrentControlSet\Control\AGP"
```

你可以在筛选器驱动程序服务密钥中的 "参数" 下找到平台特定的条目。 例如，以下位置的假设 AcmeAGP 适配器的这些条目存在于注册表中：

```registry
HKLM,"SYSTEM\CurrentControlSet\Services\AcmeAGP\Parameters"
```

若要为具有 DeviceID 的0x012A （Nuclear3D）和（通过技术平台上的0x1AD0）的设备禁用 sideband 寻址，请向 INF 文件添加**Nuclear3D\_Install**部分。 （有关此类型的 INF 安装部分的详细信息，请参阅[**Inf DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。）本部分包含如下所示的[**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)指令：

```inf
[Nuclear3D_Install.HW] 
AddReg = Nuclear3D_Reg 
```

接下来，创建以下部分，其中**AddReg**指令指向：

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
```

前面的条目指示由 HKLM 后面的字符串标识的子项将添加到注册表中的 HKEY\_本地\_计算机根下。 "1AD0012A" 字符串是输入名称，其中的前四个字符构成 DeviceID，最后四个字符组成此部分的 VendorID。 输入名称后面的十六进制数包含一组标志，指示该项的数据类型。 最后一个部分是用于禁用 sideband 寻址的条目值。

**重要**   值项中的字节与 AGP\_标志中的字节相反，\_不\_SBA\_在上表中启用标志的定义。

 

假设你确定此同一设备的每个芯片上的 AGP 4X 都已断开。 若要指示这一事实，请将第二个条目添加到 Nuclear3D\_Reg 部分：

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
HKLM,"SYSTEM\CurrentControlSet\Control\AGP","1AD0012A",0x00030003,04,00,00,00,00,00,00,00 
```

前面代码中的第二个条目指出，由 HKLM 后面的字符串标识的子项将添加到注册表中的 HKEY\_本地\_计算机根下。 与上一项一样，与此子项关联的值名称是由设备的 DeviceID 和 VendorID 组成的字符串。 标志值也相同。 值项是 AGP\_标志，\_不\_4X\_速率，这将禁用 AGP 4X 传输速率。 请注意，与之前一样，此值项中的字节的顺序与上表中标志的值相同。

 

 





