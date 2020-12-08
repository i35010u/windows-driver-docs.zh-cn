---
title: 音频驱动程序的版本号
description: 音频驱动程序的版本号
keywords:
- 版本号 WDK 音频
- 音频微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 音频适配器驱动程序 WDK，版本号
- 适配器驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，支持的模型
- 驱动程序版本号 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a78e39ca20ab0926a8ad9728d7e35911803f927
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798827"
---
# <a name="version-numbers-for-audio-drivers"></a>音频驱动程序的版本号


## <span id="version_numbers_for_audio_drivers"></span><span id="VERSION_NUMBERS_FOR_AUDIO_DRIVERS"></span>


Windows 操作系统支持三种类型的音频驱动程序模型： VxD、WDM 和 NT4 (Microsoft Windows NT 4.0) 驱动程序模型。 分配给音频适配器驱动程序的版本号取决于你使用的驱动程序型号、你面向的 Windows 版本，还可能是 Microsoft DirectX 版本。 以下四个表按驱动程序型号列出驱动程序版本号。

### <a name="span-iddriver_model__vxd_drivers_for_windows_95spanspan-iddriver_model__vxd_drivers_for_windows_95spandriver-model-vxd-drivers-for-windows-95"></a><span id="driver_model__vxd_drivers_for_windows_95"></span><span id="DRIVER_MODEL__VXD_DRIVERS_FOR_WINDOWS_95"></span>驱动程序型号： Windows 95 的 VxD 驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX 版本</th>
<th align="left">驱动程序版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>不支持 DirectX 的 Windows 95</p></td>
<td align="left"><p>4.00.00.0096 到4.02.00.0094</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX1</p></td>
<td align="left"><p>4.02.00.0096 到4.02.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DX2</p></td>
<td align="left"><p>4.03.00.1097 到4.03.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX3</p></td>
<td align="left"><p>4.04.00.1097 到4.04.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DX5</p></td>
<td align="left"><p>4.05.00.1000 到4.05.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX6</p></td>
<td align="left"><p>4.06.00.1000 到4.06.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddriver_model__vxd_drivers_for_windows_98spanspan-iddriver_model__vxd_drivers_for_windows_98spandriver-model-vxd-drivers-for-windows-98"></a><span id="driver_model__vxd_drivers_for_windows_98"></span><span id="DRIVER_MODEL__VXD_DRIVERS_FOR_WINDOWS_98"></span>驱动程序型号： Windows 98 的 VxD 驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX 版本</th>
<th align="left">驱动程序版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DX5</p></td>
<td align="left"><p>4.05.01.2500 到4.05.99.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX6</p></td>
<td align="left"><p>4.06.00.1000 到4.06.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddriver_model__wdm_drivers_for_windows_me_98__and_windows_2000_and_latespanspan-iddriver_model__wdm_drivers_for_windows_me_98__and_windows_2000_and_latespandriver-model-wdm-drivers-for-windows-me98-and-windows-2000-and-later"></a><span id="driver_model__wdm_drivers_for_windows_me_98__and_windows_2000_and_late"></span><span id="DRIVER_MODEL__WDM_DRIVERS_FOR_WINDOWS_ME_98__AND_WINDOWS_2000_AND_LATE"></span>驱动程序模型： Windows Me/98 和 Windows 2000 及更高版本的 WDM 驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">驱动程序版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98</p></td>
<td align="left"><p>4.10.00.2500 到4.10.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5.00.00.3500 到5.00.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>4.90.00.3500 到4.90.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5.10.00.3500 到5.10.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6.00.00.3500 到6.00.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>7.00.00.3500 到7.00.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>8.00.00.3500 到8.00.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddriver_model__nt4_drivers__windows_nt_4_0_only_spanspan-iddriver_model__nt4_drivers__windows_nt_4_0_only_spandriver-model-nt4-drivers-windows-nt-40-only"></a><span id="driver_model__nt4_drivers__windows_nt_4_0_only_"></span><span id="DRIVER_MODEL__NT4_DRIVERS__WINDOWS_NT_4_0_ONLY_"></span>驱动程序模型：仅限 Windows NT 4.0 (NT4 驱动程序) 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">驱动程序版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows NT 4.0</p></td>
<td align="left"><p>4.00.00.1400 到4.00.00.9999</p></td>
</tr>
</tbody>
</table>

 

对于不支持 DirectX 的设备驱动程序，版本号应大于或等于4.00.00.0096 且小于或等于4.02.00.0094。 支持 DirectX 1.0 版的设备驱动程序的版本号应在4.02.00.0096 到4.02.00.9999 的范围内。 支持更高版本 DirectX 的设备驱动程序的版本号应为适用于 DirectX 的分布式版本的范围，如前面的表中所示。

所有 WDM 驱动程序的版本号应大于或等于4.10.00.2500，这是 Windows 98 版本号范围的低端。

请注意，为早期版本的 Windows 编写的 WDM 驱动程序也会在以后的版本中正常运行。 例如，写入到 Windows 2000 中运行的 WDM 驱动程序也在 Microsoft Windows XP 和更高版本中运行。

DirectX 1.0 版驱动程序在安装了 DirectX 2.0 的系统中工作。 但是，除非安装了 DirectX 2.0，否则 DirectX 2.0 驱动程序无法正常工作。 这同样适用于 DirectX 3.0 和更高版本。

跨平台驱动程序应将其版本号设置为运行该驱动程序的平台的最高版本号。 例如，供应商应使用5.00.00 的驱动程序版本号。*Xxxx* ：支持 windows 2000、windows 98、WINDOWS 98 SE 和 windows Me 的驱动程序。

本节包括：

[内部和外部版本号](internal-and-external-version-numbers.md)

[INF Driver-Version 条目](inf-driver-version-entry.md)

[DirectX 文件版本号](directx-file-version-numbers.md)

 

 




