---
title: 显示示例
description: 显示示例
ms.assetid: 4595369c-20fa-4c8d-ad1d-aada97ab9fc2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e3918a841f55e03feeae117b372348b3c6fad80
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064854"
---
# <a name="display-samples"></a>显示示例


### <span id="display_samples"></span><span id="DISPLAY_SAMPLES"></span>

从 Windows 8 开始，可以从硬件开发人员中心 [下载示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 。 对于 Windows 7 及更早版本，示例和文档包括在 Windows 驱动程序工具包 (WDK) 或驱动程序开发工具包 (DDK) 中。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">示例名称</th>
<th align="left">生成环境</th>
<th align="left">目标操作系统</th>
<th align="left">PnP 驱动程序</th>
<th align="left">内置驱动程序</th>
<th align="left">示例说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Kernel mode display-only miniport driver](https://go.microsoft.com/fwlink/p/?LinkId=618052)">仅限内核模式显示微型端口驱动程序</a></p>
<p>在硬件开发人员中心可用。</p></td>
<td align="left"><p></p>
Windows 8</td>
<td align="left"><p></p>
Windows 8</td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>实现 (DDIs 的大多数设备驱动程序接口，) 只显示微型端口驱动程序应 (WDDM) 提供给 Windows 显示驱动程序模型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[PixLib](https://go.microsoft.com/fwlink/p/?LinkId=618052)">PixLib</a></p>
<p>在硬件开发人员中心可用。</p></td>
<td align="left"><p></p>
Windows 8 Windows 7 Windows Server 2008 Windows Vista Windows Server 2003 Windows XP</td>
<td align="left"><p></p>
Windows 8 Windows 7 Windows Server 2008 Windows Vista Windows Server 2003 Windows XP</td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>演示如何实现 <a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-support-methods-for-lightweight-mip-maps" data-raw-source="[CPixel](./cpixel-support-methods-for-lightweight-mip-maps.md)">CPixel</a> 类。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>镜像的镜像驱动程序 GDI 内容</p></td>
<td align="left"><p></p>
Windows 7 Windows Server 2008 Windows Vista Windows Server 2003 Windows XP Windows 2000</td>
<td align="left"><p></p>
Windows 7 Windows Server 2008 Windows Vista Windows Server 2003 Windows XP Windows 2000</td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>演示执行 <a href="mirror-drivers.md" data-raw-source="[video mirroring](mirror-drivers.md)">视频镜像</a>的驱动程序。</p>
<div class="alert">
<strong>注意</strong>   从 Windows 8 开始，镜像驱动程序将不会安装在系统上。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>MonINF</p></td>
<td align="left"><p></p>
Windows 7 Windows Server 2008 Windows Vista</td>
<td align="left"><p></p>
Windows 7 Windows Server 2008 Windows Vista</td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>演示监视器制造商如何通过实现覆盖软件中部分或全部 EDID 信息的监视器 INF，来避免 reflashing 监视器的 EEPROM。</p></td>
</tr>
</tbody>
</table>

 

 

