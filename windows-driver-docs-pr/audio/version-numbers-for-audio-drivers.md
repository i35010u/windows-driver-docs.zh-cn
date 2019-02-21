---
title: 音频驱动程序的版本号
description: 音频驱动程序的版本号
ms.assetid: 6d621021-eb45-40ab-9452-97c9be2bbdd8
keywords:
- 版本编号 WDK 音频
- 音频的微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 音频适配器驱动程序 WDK，版本号
- 适配器驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，支持的模型
- 驱动程序版本数字 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f228b9b65cbe0500f1b618070dded00519f62bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543043"
---
# <a name="version-numbers-for-audio-drivers"></a>音频驱动程序的版本号


## <span id="version_numbers_for_audio_drivers"></span><span id="VERSION_NUMBERS_FOR_AUDIO_DRIVERS"></span>


Windows 操作系统支持三种类型的音频驱动程序模型： VxD、 WDM 和 NT4 (Microsoft Windows NT 4.0) 驱动程序模型。 你将分配给您的声卡驱动程序的版本号取决于驱动程序模型，使用时，Windows 发布目标，并可能在 Microsoft DirectX 版本以及。 以下四个表列出了由驱动程序模型的驱动程序版本号。

### <a name="span-iddrivermodelvxddriversforwindows95spanspan-iddrivermodelvxddriversforwindows95spandriver-model-vxd-drivers-for-windows-95"></a><span id="driver_model__vxd_drivers_for_windows_95"></span><span id="DRIVER_MODEL__VXD_DRIVERS_FOR_WINDOWS_95"></span>驱动程序模型：Windows 95 的 VxD 驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX 版本</th>
<th align="left">驱动程序的版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>如果没有 DirectX 支持 windows 95</p></td>
<td align="left"><p>4.00.00.0096 到 4.02.00.0094</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX1</p></td>
<td align="left"><p>4.02.00.0096 到 4.02.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DX2</p></td>
<td align="left"><p>4.03.00.1097 到 4.03.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX3</p></td>
<td align="left"><p>4.04.00.1097 到 4.04.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DX5</p></td>
<td align="left"><p>4.05.00.1000 到 4.05.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX6</p></td>
<td align="left"><p>4.06.00.1000 到 4.06.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddrivermodelvxddriversforwindows98spanspan-iddrivermodelvxddriversforwindows98spandriver-model-vxd-drivers-for-windows-98"></a><span id="driver_model__vxd_drivers_for_windows_98"></span><span id="DRIVER_MODEL__VXD_DRIVERS_FOR_WINDOWS_98"></span>驱动程序模型：Windows 98 的 VxD 驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX 版本</th>
<th align="left">驱动程序的版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DX5</p></td>
<td align="left"><p>4.05.01.2500 到 4.05.99.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX6</p></td>
<td align="left"><p>4.06.00.1000 到 4.06.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddrivermodelwdmdriversforwindowsme98andwindows2000andlatespanspan-iddrivermodelwdmdriversforwindowsme98andwindows2000andlatespandriver-model-wdm-drivers-for-windows-me98-and-windows-2000-and-later"></a><span id="driver_model__wdm_drivers_for_windows_me_98__and_windows_2000_and_late"></span><span id="DRIVER_MODEL__WDM_DRIVERS_FOR_WINDOWS_ME_98__AND_WINDOWS_2000_AND_LATE"></span>驱动程序模型：WDM 驱动程序的 Windows Me / 98 和 Windows 2000 及更高版本

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">驱动程序的版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98</p></td>
<td align="left"><p>4.10.00.2500 到 4.10.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5.00.00.3500 到 5.00.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>4.90.00.3500 到 4.90.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5.10.00.3500 到 5.10.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6.00.00.3500 到 6.00.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>7.00.00.3500 到 7.00.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>8.00.00.3500 到 8.00.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddrivermodelnt4driverswindowsnt40onlyspanspan-iddrivermodelnt4driverswindowsnt40onlyspandriver-model-nt4-drivers-windows-nt-40-only"></a><span id="driver_model__nt4_drivers__windows_nt_4_0_only_"></span><span id="DRIVER_MODEL__NT4_DRIVERS__WINDOWS_NT_4_0_ONLY_"></span>驱动程序模型：NT4 驱动程序 (Windows NT 4.0 仅)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">驱动程序的版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows NT 4.0</p></td>
<td align="left"><p>4.00.00.1400 到 4.00.00.9999</p></td>
</tr>
</tbody>
</table>

 

不支持 DirectX 的设备驱动程序，版本号应该是大于或等于 4.00.00.0096 且小于或等于 4.02.00.0094。 支持 DirectX 版本 1.0 的设备驱动程序应具有在范围内 4.02.00.0096 到 4.02.00.9999 版本号。 支持更高版本的 DirectX 的设备驱动程序应具有版本号适用于分布式版本的 DirectX，范围中前面的表中所示。

所有 WDM 驱动程序应都具有版本号大于或等于 4.10.00.2500，这是 Windows 98 版本数量范围的低端。

请注意，对于 Windows 的早期版本编写的 WDM 驱动程序以及更高版本上正确运行。 例如，编写为在 Windows 2000 中运行的 WDM 驱动程序还在运行 Microsoft Windows XP 及更高版本。

DirectX 版本 1.0 驱动程序在系统中使用安装的 DirectX 2.0。 但是，除非安装 DirectX 2.0 DirectX 2.0 驱动程序执行操作无法正常工作。 同样适用于 DirectX 3.0 和更高版本。

跨平台驱动程序应设置其版本号为驱动程序在其运行的平台的最高版本号。 例如，一个供应商应使用 5.00.00 驱动程序版本号。*Xxxx*驱动程序支持 Windows 2000、 Windows 98 和 Windows 98 SE、 Windows me 一起提供。

本部分包括：

[内部和外部的版本号](internal-and-external-version-numbers.md)

[INF 驱动程序版本条目](inf-driver-version-entry.md)

[DirectX 文件版本号](directx-file-version-numbers.md)

 

 




