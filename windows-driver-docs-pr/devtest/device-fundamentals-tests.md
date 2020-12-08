---
title: 设备基础功能测试
description: 设备基础测试的说明。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7acde44781a21ff4ceffb15f6d9673b0d4cfb8c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836529"
---
# <a name="device-fundamentals-tests"></a>设备基础功能测试


## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="chaos-tests--device-fundamentals-.md" data-raw-source="[CHAOS Tests (Device Fundamentals)](chaos-tests--device-fundamentals-.md)">混沌测试（设备基础功能）</a></p></td>
<td align="left"><p> (并发硬件和操作系统的混乱) 测试会同时运行各种 PnP 驱动程序测试、设备驱动程序模糊测试和电源系统测试。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="coverage-tests--device-fundamentals-.md" data-raw-source="[Coverage Tests (Device Fundamentals)](coverage-tests--device-fundamentals-.md)">覆盖范围测试（设备基础功能）</a></p></td>
<td align="left"><p>设备基础覆盖率测试监视和报告各种 i/o 请求数据包 (Irp) 为指定设备进入或离开驱动程序堆栈。 覆盖率测试中的数据可帮助确定驱动程序测试和验证过程中的覆盖率弱点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpustress-tests--device-fundamentals-.md" data-raw-source="[CPUStress Tests (Device Fundamentals)](cpustress-tests--device-fundamentals-.md)">CPU 压力测试（设备基础功能）</a></p></td>
<td align="left"><p>CpuStress 测试将执行具有不同处理器利用率级别的设备 i/o 测试。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driverinstall-tests--device-fundamentals-.md" data-raw-source="[DriverInstall Tests (Device Fundamentals)](driverinstall-tests--device-fundamentals-.md)">驱动程序安装测试（设备基础功能）</a></p></td>
<td align="left"><p>驱动程序安装测试类别包括多次卸载和重新安装驱动程序以测试安装功能的测试。 每次重新安装之后，这些测试将启动针对驱动程序和设备的 i/o 测试。 这些测试旨在提高需要安装和重新安装设备驱动程序或设备的最终用户的总体体验。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="i-o-tests--device-fundamentals-.md" data-raw-source="[I/O Tests (Device Fundamentals)](i-o-tests--device-fundamentals-.md)">I/O 测试（设备基础功能）</a></p></td>
<td align="left"><p>设备基础 i/o 测试在指定设备上执行基本 i/o 测试。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="penetration-tests--device-fundamentals-.md" data-raw-source="[Penetration Tests (Device Fundamentals)](penetration-tests--device-fundamentals-.md)">渗透压力测试（设备基础功能）</a></p></td>
<td align="left"><p>设备基础的渗透测试执行各种形式的输入攻击，这是安全测试的关键组成部分。 攻击和渗透测试可帮助识别软件接口中的漏洞。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="pnp-tests--device-fundamentals-.md" data-raw-source="[PnP Tests (Device Fundamentals)](pnp-tests--device-fundamentals-.md)">PnP 测试（设备基础功能）</a></p></td>
<td align="left"><p>设备基础知识 PnP 测试强制驱动程序处理几乎所有 PnP Irp;不过，有三个区域特别明显：删除、重新平衡和意外删除。 PnP 测试提供一种机制，用于单独测试每个测试，或将它们一起进行测试 (即) 压力测试。 此 PnP 测试通过结合使用用户模式 API 调用 (来完成：通过测试应用程序) 和内核模式 API 调用 (通过) 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="reboot-tests--device-fundamentals-.md" data-raw-source="[Reboot Tests (Device Fundamentals)](reboot-tests--device-fundamentals-.md)">重新启动测试（设备基础功能）</a></p></td>
<td align="left"><p>设备基础重新启动测试在指定的设备上、之前和之后或在系统重启期间运行 i/o。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="sleep-tests--device-fundamentals-.md" data-raw-source="[Sleep Tests (Device Fundamentals)](sleep-tests--device-fundamentals-.md)">睡眠测试（设备基础功能）</a></p></td>
<td align="left"><p>设备基础睡眠测试在指定的设备上、之前和之后或在系统睡眠状态转换期间运行 i/o 和 PnP 操作。 睡眠测试可确保所测试的设备能够通过所有受支持的睡眠状态进行循环。 此外，它还可以确保在这些状态发生更改后，设备仍能正常运行，这是因为简单的 i/o 压力测试。</p></td>
</tr>
</tbody>
</table>

 

 

 





