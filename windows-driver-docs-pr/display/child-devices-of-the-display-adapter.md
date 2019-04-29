---
title: 显示适配器的子设备
description: 显示适配器的子设备
ms.assetid: 9fd20e1a-db98-4571-8fc4-6d33fd0e2f16
keywords:
- 视频存在网络 WDK 显示，显示适配器子设备
- VidPN WDK 显示，显示适配器子设备
- 子设备 WDK 视频存在网络
- 显示适配器子设备 WDK 视频存在网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07cb1882314d685b120e308037ce35f0d7e2240d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354336"
---
# <a name="child-devices-of-the-display-adapter"></a>显示适配器的子设备


显示适配器的子设备是设备上的显示适配器的微型端口驱动程序枚举作为子级。 显示适配器的所有子设备都均载入;监视器和其他外部连接到设备的显示适配器不会考虑子设备。

显示微型端口驱动程序[ **DxgkDdiQueryChildRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff559750)函数负责枚举子设备的显示适配器。 在枚举过程显示微型端口驱动程序将指定的每个子设备类型和热插拔检测 (HPD) 感知值。 类型为之一[ **DXGK\_子\_设备\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff561008)枚举器：

-   **TypeVideoOutput**

-   **TypeOther**

HPD 感知值是之一[ **DXGK\_子\_设备\_HPD\_感知**](https://msdn.microsoft.com/library/windows/hardware/ff561006)枚举器：

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

下表提供了各种类型和 HPD 感知值的设备的一些示例。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HpdAwareness</th>
<th align="left">VideoOutput</th>
<th align="left">其他</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>AlwaysConnected</strong></p></td>
<td align="left"><p>台式计算机上的集成 LCD 面板的输出</p></td>
<td align="left"><p>电视调谐器</p>
<p>跨条形开关</p>
<p>MPEG2 编解码器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>可中断</strong></p></td>
<td align="left"><p>DVI</p>
<p>HDMI</p>
<p>集成的 LCD 面板在便携式计算机上的输出</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>轮询一次</strong></p></td>
<td align="left"><p>S-视频</p>
<p>HD15</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

操作系统使用几种策略，具体取决于 HPD 感知值之一来确定是否将外部设备连接到子设备。 下表简要介绍如何在操作系统确定的各种 HPD 感知值与设备的连接状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HpdAwareness</th>
<th align="left">操作系统如何确定连接状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AlwaysConnected</p></td>
<td align="left"><p>操作系统能识别子设备将始终存在。 没有外部设备会连接到或从子设备断开连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可中断</p></td>
<td align="left"><p>连接到或从子设备断开连接的外部显示设备时，会通知操作系统。 （在便携式计算机上的显示面板被视为连接合上盖子处于打开状态时，合上盖子时，断开连接。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>轮询一次</p></td>
<td align="left"><p>操作系统要求的外部显示设备是否已连接到子设备。</p></td>
</tr>
</tbody>
</table>

 

 

 





