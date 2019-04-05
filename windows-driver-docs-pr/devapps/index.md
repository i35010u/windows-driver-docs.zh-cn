---
title: UWP 设备应用
description: UWP 设备应用是设备的配套应用，其功能超出常规的 UWP 应用，可执行特权操作，例如固件更新
ms.assetid: fb64bad6-aa3d-4718-b62e-68da59a07ced
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: d03be44449997123f360af63887e4d5165d6bd06
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350184"
---
# <a name="uwp-device-apps"></a>UWP 设备应用


## <a name="span-idpurposespanpurpose"></a><span id="purpose"></span>用途


设备制造商可以创建用作设备配套的 UWP 设备应用。 UWP 设备应用的功能超出常规的 UWP 应用，可执行特权操作，例如固件更新。 此外，UWP 设备应用可以从自动播放开始（其可以使用的设备数量超出其他应用）、在第一次连接设备时自动进行安装，并可扩展内置于 Windows 8.1 和 Windows 10 中的打印机和相机体验。

本部分介绍什么是 UWP 设备应用，以及设备制造商如何创建它们。 如果是初次接触 UWP 设备应用，请参阅[入门](getting-started.md)。

若要了解 UWP 移动宽带应用，请参阅 [Mobile Broadband](https://go.microsoft.com/fwlink/p/?LinkID=301754)（移动宽带）。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="what-s-new.md" data-raw-source="[What's new](what-s-new.md)">新增功能</a></p></td>
<td align="left"><p>本部分概述 UWP 设备应用的新增功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="getting-started.md" data-raw-source="[Getting started](getting-started.md)">入门</a></p></td>
<td align="left"><p>从这里开始构建 UWP 设备应用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="build-a-uwp-device-app-step-by-step.md" data-raw-source="[Build a UWP device app step-by-step](build-a-uwp-device-app-step-by-step.md)">分步构建 UWP 设备应用</a></p></td>
<td align="left"><p>此分步指南详细介绍了如何使用 Microsoft Visual Studio 和设备元数据创作向导构建 UWP 设备应用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay for UWP device apps](autoplay-for-uwp-device-apps.md)">UWP 设备应用的自动播放</a></p></td>
<td align="left"><p>本主题介绍如何使用设备元数据创作向导来启用自动播放。 它还介绍了如何在应用中处理自动播放激活。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="device-sync-and-update-for-uwp-device-apps.md" data-raw-source="[Device sync and update for UWP device apps](device-sync-and-update-for-uwp-device-apps.md)">UWP 设备应用的设备同步和更新</a></p></td>
<td align="left"><p>在 Windows 8.1 中，UWP 应用可以使用设备后台任务来同步外围设备上的数据。 如果应用与设备元数据相关联，则该 UWP 设备应用还可以使用设备后台代理进行设备更新，例如固件更新。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="uwp-device-apps-for-printers.md" data-raw-source="[UWP device apps for printers](uwp-device-apps-for-printers.md)">打印机的 UWP 设备应用</a></p></td>
<td align="left"><p>此部分介绍打印机的 UWP 设备应用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="uwp-device-apps-for-webcams.md" data-raw-source="[UWP device apps for cameras](uwp-device-apps-for-webcams.md)">适用于相机的 UWP 设备应用</a></p></td>
<td align="left"><p>此部分介绍相机的 UWP 设备应用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="uwp-device-apps-for-specialized-devices.md" data-raw-source="[UWP device apps for internal devices](uwp-device-apps-for-specialized-devices.md)">适用于内部设备的 UWP 设备应用</a></p></td>
<td align="left"><p>此主题介绍 UWP 设备应用访问内部设备的方式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="auto-install-for-uwp-device-apps.md" data-raw-source="[Automatic installation for UWP device apps](auto-install-for-uwp-device-apps.md)">UWP 设备应用的自动安装</a></p></td>
<td align="left"><p>本主题介绍如何进行自动安装，以及如何更新和卸载应用、元数据和驱动程序。</p></td>
</tr>
</tr>
<tr class="even">
<td align="left"><p><a href="hardware-support-app--hsa--steps-for-driver-developers.md" data-raw-source="[Hardware Support App (HSA): Steps for Driver Developers](hardware-support-app--hsa--steps-for-driver-developers.md)">硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤</a></p></td>
<td align="left"><p>此主题为开发人员提供将驱动程序与通用 Windows 平台 (UWP) 应用关联的步骤。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-support-app--hsa--steps-for-app-developers.md" data-raw-source="[Hardware Support App (HSA): Steps for App Developers](hardware-support-app--hsa--steps-for-app-developers.md)">硬件支持应用 (HSA)：适用于应用开发人员的步骤</a></p></td>
<td align="left"><p>此主题为应用开发人员提供将通用 Windows 平台 (UWP) 应用与通用 Windows 驱动程序关联的步骤。</p></td>
</tr>
</tbody>
</table>

 

 

 





