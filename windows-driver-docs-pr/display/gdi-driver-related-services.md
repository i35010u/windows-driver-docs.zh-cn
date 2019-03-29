---
title: GDI 驱动程序相关服务
description: GDI 驱动程序相关服务
ms.assetid: bb46ae7a-9ade-4e23-b9fe-489f83445ff3
keywords:
- GDI WDK Windows 2000 显示，与驱动程序相关的服务
- 图形驱动程序 WDK Windows 2000 显示，与驱动程序相关的服务
- 绘制 WDK GDI，与驱动程序相关的服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df50d246e0ca1113de98078dd87d264874363671
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350326"
---
# <a name="gdi-driver-related-services"></a>GDI 驱动程序相关服务


## <span id="ddk_gdi_driver_related_services_gg"></span><span id="DDK_GDI_DRIVER_RELATED_SERVICES_GG"></span>


驱动程序编写人员可以使用下表中列出的 GDI 驱动程序相关服务来创建或删除驱动程序对象，获取驱动程序的 DLL 的名称和锁定或解锁驱动程序对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564207" data-raw-source="[&lt;strong&gt;EngCreateDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564207)"><strong>EngCreateDriverObj</strong></a></p></td>
<td align="left"><p>创建<a href="https://msdn.microsoft.com/library/windows/hardware/ff556162" data-raw-source="[&lt;strong&gt;DRIVEROBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556162)"> <strong>DRIVEROBJ</strong> </a>结构。 此结构用于跟踪设备管理的资源分配进程是否终止，而又没有第一个清理它必须释放的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564792" data-raw-source="[&lt;strong&gt;EngDeleteDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564792)"><strong>EngDeleteDriverObj</strong></a></p></td>
<td align="left"><p>释放句柄用于跟踪设备管理的资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564927" data-raw-source="[&lt;strong&gt;EngGetDriverName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564927)"><strong>EngGetDriverName</strong></a></p></td>
<td align="left"><p>返回驱动程序的 DLL 的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564967" data-raw-source="[&lt;strong&gt;EngLockDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564967)"><strong>EngLockDriverObj</strong></a></p></td>
<td align="left"><p>在调用线程的驱动程序对象上创建的排他锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565044" data-raw-source="[&lt;strong&gt;EngUnlockDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565044)"><strong>EngUnlockDriverObj</strong></a></p></td>
<td align="left"><p>解除锁定的驱动程序对象。</p></td>
</tr>
</tbody>
</table>

 

 

 





