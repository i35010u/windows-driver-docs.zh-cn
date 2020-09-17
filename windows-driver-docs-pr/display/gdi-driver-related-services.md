---
title: GDI 驱动程序相关服务
description: GDI 驱动程序相关服务
ms.assetid: bb46ae7a-9ade-4e23-b9fe-489f83445ff3
keywords:
- GDI WDK Windows 2000 显示器、驱动程序相关服务
- 图形驱动程序 WDK Windows 2000 显示器、驱动程序相关服务
- 绘制 WDK GDI、驱动程序相关服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb06e290e35cfff7ad1f817ce0fe7c43235827c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716486"
---
# <a name="gdi-driver-related-services"></a>GDI 驱动程序相关服务


## <span id="ddk_gdi_driver_related_services_gg"></span><span id="DDK_GDI_DRIVER_RELATED_SERVICES_GG"></span>


驱动程序编写者可以使用下表中列出的 GDI 驱动程序相关服务来创建或删除驱动程序对象，获取驱动程序的 DLL 的名称，以及锁定或解锁驱动程序对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatedriverobj" data-raw-source="[&lt;strong&gt;EngCreateDriverObj&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatedriverobj)"><strong>EngCreateDriverObj</strong></a></p></td>
<td align="left"><p>创建 <a href="/windows/win32/api/winddi/ns-winddi-_driverobj" data-raw-source="[&lt;strong&gt;DRIVEROBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_driverobj)"><strong>DRIVEROBJ</strong></a> 结构。 此结构用于跟踪设备托管的资源，如果在资源分配进程终止的情况下终止该资源，则该资源必须释放。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletedriverobj" data-raw-source="[&lt;strong&gt;EngDeleteDriverObj&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletedriverobj)"><strong>EngDeleteDriverObj</strong></a></p></td>
<td align="left"><p>释放用于跟踪设备托管资源的句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggetdrivername" data-raw-source="[&lt;strong&gt;EngGetDriverName&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggetdrivername)"><strong>EngGetDriverName</strong></a></p></td>
<td align="left"><p>返回驱动程序 DLL 的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-englockdriverobj" data-raw-source="[&lt;strong&gt;EngLockDriverObj&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-englockdriverobj)"><strong>EngLockDriverObj</strong></a></p></td>
<td align="left"><p>为调用线程创建驱动程序对象上的排他锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunlockdriverobj" data-raw-source="[&lt;strong&gt;EngUnlockDriverObj&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunlockdriverobj)"><strong>EngUnlockDriverObj</strong></a></p></td>
<td align="left"><p>解锁驱动程序对象。</p></td>
</tr>
</tbody>
</table>

 

