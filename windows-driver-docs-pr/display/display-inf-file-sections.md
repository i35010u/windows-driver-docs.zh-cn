---
title: 显示 INF 文件节
description: 显示 INF 文件节
ms.assetid: 2075a10f-a504-4bdc-8112-9c583c5084bb
keywords:
- 旁带寻址 WDK Windows 2000 显示
- AGP 传输速率 WDK Windows 2000 显示
- SoftwareSettings 部分
- CapabilityOverride
- INF 文件 WDK Windows 2000 显示
- 显示 INF 文件部分 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dad82914b5609af854bdf82d05f037219a045681
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382933"
---
# <a name="display-inf-file-sections"></a>显示 INF 文件节


## <span id="ddk_display_inf_file_sections_gg"></span><span id="DDK_DISPLAY_INF_FILE_SECTIONS_GG"></span>


此节介绍了如何编写安装程序信息文件 (INF) 部分专门适用于图形适配器安装。 INF 文件有关的更多常规信息，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

### <a name="span-idddinstallsoftwaresettingssectionspanspan-idddinstallsoftwaresettingssectionspanspan-idddinstallsoftwaresettingssectionspanddinstallsoftwaresettings-section"></a><span id="DDInstall.SoftwareSettings_Section"></span><span id="ddinstall.softwaresettings_section"></span><span id="DDINSTALL.SOFTWARESETTINGS_SECTION"></span>DDInstall.SoftwareSettings 部分

一个*DDInstall*。**SoftwareSettings**部分包含[ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)指令和/或[ **DelReg** ](https://msdn.microsoft.com/library/windows/hardware/ff547374)指令。 每个指令指向单独编写器定义 INF 部分，其中包含的安装程序以添加或删除注册表项。

例如，下面的代码演示**AddReg**指令指向一个名为的编写器定义添加的注册表部分**ACME 1234\_SoftwareDeviceSettings**。 **DelReg**指令指向一个名为删除注册表部分**ACME 1234\_DeleteSWSettings**。

```inf
[ACME-1234.SoftwareSettings]
AddReg=ACME-1234_SoftwareDeviceSettings
DelReg=ACME-1234_DeleteSWSettings
```

添加注册表部分将四个条目添加到注册表，并设置它们的值，如下面的代码中所示。

```inf
[ACME-1234_SoftwareDeviceSettings]
HKR,, InstalledDisplayDrivers, %REG_MULTI_SZ%, Acme1
HKR,, OverRideMonitorPower, %REG_DWORD%, 0
HKR,, MultiFunctionSupported, %REG_DWORD%, 1
HKR,, VideoDebugLevel, %REG_DWORD%, 2
```

前面的代码首先设置的值**InstalledDisplayDrivers**进入显示器驱动程序的名称。 代码随后设置的值**OverRideMonitorPower**为 0 (即**FALSE**)。 此条目，应仅由 OEM 系统供应商合作，控制监视设备 （例如，LCD、 CRT 或电视） 的 power 行为。 如果设置为 1， **OverRideMonitorPower**限制到 D0 和 D3 监视设备的可能的电源状态。

第三，该代码设置的值**MultiFunctionSupported**为 1 的条目 (换而言之， **TRUE**)，这是所需的适配器支持多个 PCI 函数的值。 最后，该代码设置的值**VideoDebugLevel**条目，控制检查生成用于调试消息的全局调试级别。 此值为 3 （最详细的消息） 的范围从 0 （不调试消息）。 有关全局调试级别的详细信息，请参阅[ **VideoDebugPrint**](https://msdn.microsoft.com/library/windows/hardware/ff570170)。

大多数视频微型端口驱动程序不是兼容的 VGA，需要无**VgaCompatible**的注册表项。 如果您的微型端口驱动程序兼容的 VGA，请添加**VgaCompatible**注册表项并将其值设置为 1 (**TRUE**) 中添加的注册表部分，如下所示：

```registry
[ACME-1234_SoftwareDeviceSettings]
HKR,, VgaCompatible, %REG_DWORD%, 1
```

有关兼容的 VGA 的微型端口驱动程序的详细信息，请参阅[兼容的 VGA 视频微型端口驱动程序 （Windows 2000 模式）](vga-compatible-video-miniport-drivers--windows-2000-model-.md)。

以下部分中删除注册表中删除三个注册表项：**GraphicsClocking**， **MemClocking**，和**CapabilityOverride**。

```inf
[ACME-1234_DeleteSWSettings]
HKR,, GraphicsClocking
HKR,, MemClocking
HKR,, CapabilityOverride
```

**CapabilityOverride**条目指定对显示驱动程序将关闭系统的功能。 例如，即使显示驱动程序实现[ **DrvEscape** ](https://msdn.microsoft.com/library/windows/hardware/ff556217)函数，如果设置了 0x10 标志不能使用功能**CapabilityOverride**条目。

值**CapabilityOverride**注册表项是一个或多个以下表中列出的标志的按位 OR。

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
<td align="left"><p>禁用所有硬件加速。 等效于移动硬件加速滑动条 (在<strong>显示</strong>控制面板项) 到最小设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>禁用所有支持 Microsoft DirectDraw 和 Microsoft Direct3D 硬件加速。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>禁用所有支持 Direct3D 硬件加速。 可防止对调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549404" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549404)"> <strong>DdGetDriverInfo</strong></a><em>，</em>哪一到达该驱动程序请求 Direct3D 功能和回调信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>禁用所有支持 OpenGL 可安装的客户端驱动程序 (ICD) 和 miniclient 驱动程序 (MCD)。 可防止对调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff556285" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556285)"> <strong>DrvSetPixelFormat</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff556190" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556190)"> <strong>DrvDescribePixelFormat</strong></a>，并<a href="https://msdn.microsoft.com/library/windows/hardware/ff556322" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556322)"> <strong>DrvSwapBuffers</strong> </a>到达该驱动程序。 此外可以防止 OPENGL_GETINFO、 OPENGL_CMD 和 MCDFUNCS 转义到达该驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>禁止支持人员的驱动程序中的所有转义符。 可防止对调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff556217" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556217)"> <strong>DrvEscape</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff556203" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556203)"> <strong>DrvDrawEscape</strong> </a>到达该驱动程序。</p></td>
</tr>
</tbody>
</table>

 

随 Windows，附带的显示器驱动程序的**CapabilityOverride**通常设置为 0x8，这将禁用 OpenGL。 请注意，不需要设置 0x10 标志禁用 OpenGL，除非您想要禁用所有转义符，不应设置 0x10 标志。

Microsoft Windows XP 和早期版本的操作系统不删除**CapabilityOverride**注册表项时显示驱动程序更新时间--例如，从与 Windows 传送到提供的较新驱动程序的驱动程序独立硬件供应商 (IHV)。 持久**CapabilityOverride**条目禁用更新其在旧驱动程序中禁用的驱动程序中的相同功能。 因此，对于 Windows XP 及更早版本，包括**DelReg**显式删除现有的 INF 文件中指令**CapabilityOverride**条目。 Windows XP SP1 和更高版本操作系统会自动删除**CapabilityOverride**条目，因此，对于这些系统，它不删除所需更新驱动程序时**CapabilityOverride**项。

### <a name="span-iddisablingagptransferratesandsidebandaddressingspanspan-iddisablingagptransferratesandsidebandaddressingspanspan-iddisablingagptransferratesandsidebandaddressingspandisabling-agp-transfer-rates-and-sideband-addressing"></a><span id="Disabling_AGP_Transfer_Rates_and_Sideband_Addressing"></span><span id="disabling_agp_transfer_rates_and_sideband_addressing"></span><span id="DISABLING_AGP_TRANSFER_RATES_AND_SIDEBAND_ADDRESSING"></span>禁用 AGP 传输速率和旁带寻址

如有必要，可以修改您的显示适配器禁用某些 AGP 传输速率或旁带寻址的 INF 文件。 请注意，它将调用时，微型端口驱动程序可以更改 AGP 传输速率[ **AgpSetRate**](https://msdn.microsoft.com/library/windows/hardware/ff538226)，但不是允许此类调用以更改 INF 文件中禁用的传输速率。

*Regstr.h*头文件，它提供与 Windows Driver Kit (WDK) 中，定义以下一组标志。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_1X_RATE</p></td>
<td align="left"><p>0x00000001L</p></td>
<td align="left"><p>禁用单速度 (66 MHz) 传输速率。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_2X_RATE</p></td>
<td align="left"><p>0x00000002L</p></td>
<td align="left"><p>禁用两次的单速度传输速率。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_4X_RATE</p></td>
<td align="left"><p>0x00000004L</p></td>
<td align="left"><p>禁用四次单速度传输速率。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_8X_RATE</p></td>
<td align="left"><p>0x00000008L</p></td>
<td align="left"><p>禁用八次单速度传输速率。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_SBA_ENABLE</p></td>
<td align="left"><p>0x00000100L</p></td>
<td align="left"><p>禁用旁带寻址 (SBA)。</p></td>
</tr>
</tbody>
</table>

 

存在两种类型的设置： 全局和特定于平台的。 注册表包含全局项上的以下位置：

```registry
HKLM,"SYSTEM\CurrentControlSet\Control\AGP"
```

在筛选器驱动程序服务密钥，可以找到"参数"下的特定于平台的条目。 例如，假设 AcmeAGP 适配器在注册表中的以下位置中存在这些项：

```registry
HKLM,"SYSTEM\CurrentControlSet\Services\AcmeAGP\Parameters"
```

若要禁用旁带寻址，并且在 0x012A (Nuclear3D) 的 DeviceID 0x1AD0 VendorID 通过技术平台上的设备，请添加**Nuclear3D\_Install.HW** INF 文件部分。 (有关此类型的 INF 安装部分的详细信息，请参阅[ **INF DDInstall.HW 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)。)在本部分中，包括[ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)类似于以下指令：

```inf
[Nuclear3D_Install.HW] 
AddReg = Nuclear3D_Reg 
```

接下来，创建以下部分中，其中**AddReg**指令指向：

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
```

上一项指示由以下 HKLM 字符串标识的子项是添加到注册表中，在 HKEY\_本地\_机根。 "1AD0012A"字符串是从其前四个字符构成 DeviceID，条目名称和最后四个撰写的此部分 VendorID。 项名称后面的十六进制数包含一组标志，指示该条目的数据类型。 最后一个部分是项值，这将禁用旁带寻址。

**重要**  值项中的字节是的 AGP 相反的顺序\_标志\_否\_SBA\_启用上表中的标志的定义。

 

假设您确定 AGP 4 X 在此同一设备的每个芯片集上中断。 若要指示这一事实，请将第二个条目添加到 Nuclear3D\_Reg 部分：

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
HKLM,"SYSTEM\CurrentControlSet\Control\AGP","1AD0012A",0x00030003,04,00,00,00,00,00,00,00 
```

在前面的代码的第二个条目指示由以下 HKLM 字符串标识的子项是添加到注册表中，在 HKEY\_本地\_机根。 如下所示的以前的条目，此子项与关联的值名称是由设备的 DeviceID 和 VendorID 组成的字符串。 标志值也是相同的。 值项是的 AGP\_标志\_否\_4 X\_速率，这将禁用 AGP 4 X 传输速率。 请注意，因为之前，此值条目中的字节是上表中的标志的值的顺序相反。

 

 





