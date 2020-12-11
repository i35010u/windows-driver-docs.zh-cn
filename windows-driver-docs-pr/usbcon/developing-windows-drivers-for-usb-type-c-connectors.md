---
description: 如果 USB 类型 C 系统不包含嵌入式控制器，则需要为连接器编写驱动程序，否则，可以加载 Microsoft 提供的 UCSI 驱动程序。
title: 为 USB 类型 C 连接器开发 Windows 驱动程序的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8fb1893dfc024fb745c7362b306657f9ccd28c5
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090806"
---
# <a name="overview-of-developing-windows-drivers-for-usb-type-c-connectors"></a>为 USB 类型 C 连接器开发 Windows 驱动程序的概述

如果 USB 类型 C 系统未实现 PD 状态机或它实现了状态机，但不支持通过非 ACPI 传输的 UCSI，则需要为连接器编写驱动程序。 如果是这样，可以加载 Microsoft 提供的 [UCSI 驱动程序](ucsi.md)。

**目标受众**

-   USB 类型 C 系统的驱动程序开发指南不包含嵌入式控制器。

**上次更新时间**

-   2018 年 9 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

**重要的 API**

-   [USB 类型 C 驱动程序参考](/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

![驱动程序](images/drivers-c.png)


|             硬件/固件功能             |                                                                                                                                                    不可分离                                                                                                                                                    |                                                                                                                              附加卡                                                                                                                               |
|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| USB 类型 C 连接器没有 PD 状态机。 |        [将客户端驱动程序写入 UcmTcpciCx](./write-a-usb-type-c-port-controller-driver.md)。 <p>[UcmTcpciCx 端口控制器客户端驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample)入门 </p>        | [将客户端驱动程序写入 UcmCx](./bring-up-a-usb-type-c-connector-on-a-windows-system.md)。 <p>从 [UcmCx 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)开始。</p> |
|         连接器与 ACPI 兼容 UCSI。         |                                                          加载内置驱动程序、UcmUcsiCx.sys 和 UcmUcsiAcpiClient。 请参阅 [USB Type-C 连接器系统软件接口 (UCSI) 驱动程序](./ucsi.md)。                                                           |                                                                                                                                  空值                                                                                                                                   |
|       连接器在不 UCSI 的情况下兼容。        | 将客户端驱动程序写入 UcmUcsiCx。 有关详细信息，请参阅 [编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)。 <p>[从此示例模板](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)开始，并将 ACPI 部分替换为所需总线的实现。 |                                                           [将客户端驱动程序写入 UcmCx](./bring-up-a-usb-type-c-connector-on-a-windows-system.md)。                                                            |
|    具有 PD 状态的计算机，但不符合 UCSI。     |                          [将客户端驱动程序写入 UcmCx](./bring-up-a-usb-type-c-connector-on-a-windows-system.md)。 <p>从 [UcmCx 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)开始。                          | [将客户端驱动程序写入 UcmCx](./bring-up-a-usb-type-c-connector-on-a-windows-system.md)<p>从 [UcmCx 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)开始。 </p>  |

## <a name="in-this-section"></a>在本节中
若要实现上表中建议的解决方案，请阅读以下主题：
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="architecture--usb-type-c-in-a-windows-system.md" data-raw-source="[Architecture: USB Type-C design for a Windows system](architecture--usb-type-c-in-a-windows-system.md)">体系结构：Windows 系统的 USB 类型 C 设计</a></p></td>
<td><p>介绍 USB 类型 C 系统和 Microsoft 提供的支持硬件组件的驱动程序的典型硬件设计。</p></td>
</tr>
<tr class="even">
<td><p><a href="function-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the function controller on a USB Type-C Windows system](function-controller-bringup-for-a-usb-type-c-system.md)">在 USB 类型 C Windows 系统上启动功能控制器</a></p></td>
<td><p>函数控制器的驱动程序将通知操作系统其 USB 类型 C 连接器支持的收费级别，并在电池可能开始充电时通知电池子系统，并通知设备可以消耗的最大电流。</p></td>
</tr>
<tr class="odd">
<td><p><a href="dual-role-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the dual-role controller for a USB Type-C Windows system](dual-role-controller-bringup-for-a-usb-type-c-system.md)">为 USB 类型 C Windows 系统启动双角色控制器</a></p></td>
<td><p>USB 角色切换驱动程序 (URS) 是一组 WDF 类扩展，以及处理双重角色控制器的角色切换功能的客户端驱动程序。 如果你的系统具有双重角色控制器，则你可以根据连接到系统的 USB 类型 C 连接器的合作伙伴端口的设备，来切换系统的角色。 这就允许有兴趣的方案，如有线停靠。</p></td>
</tr>
<tr class="even">
<td><p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">编写 USB 类型 C 连接器驱动程序</a></p></td>
<td><p>介绍 USB 连接器管理器 (UCM) ，该管理器管理 USB C # C 连接器和连接器驱动程序的预期行为。</p></td>
</tr>
<tr class="odd">
<td><p><a href="write-a-usb-type-c-port-controller-driver.md" data-raw-source="[Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md)">编写 USB 类型 C 端口控制器驱动程序</a></p></td>
<td><p>介绍如何编写与不带 PD 状态机的 USB 类型 C 连接器通信的 USB C # 端口控制器驱动程序。 </p></td>

</tr>
<tr class="even">
<td><p><a href="write-a-ucsi-driver.md" data-raw-source="[Write a UCSI client driver](write-a-ucsi-driver.md)">编写 UCSI 客户端驱动程序</a></p></td>
<td><p>描述如何为使用非 ACPI 传输的 UCSI 兼容控制器编写驱动程序。 </p></td>

</tr>

<tr>
<tr class="odd">
<td><a href="policy-manager-client.md" data-raw-source="[Write a USB Type-C Policy Manager client driver](policy-manager-client.md)">编写 USB 类型 C 策略管理器客户端驱动程序</a></td>
<td>Microsoft 提供的 USB 类型-C 策略管理器监视 USB 类型 C 连接器的活动。 Windows 版本1809引入了一组编程接口，可用于将客户端驱动程序写入到策略管理器。 客户端驱动程序可参与 USB C # C 连接器的策略决策。 使用此设置，可以选择写入内核模式导出驱动程序或用户模式驱动程序。 </td>
</tbody>
</table>



**相关章节**

[) 客户端驱动程序 (URS 写入 USB 角色切换 ](usb-dual-role-driver-stack-architecture.md)

[USB 双角色控制器驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

[写入 USB 函数客户端驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  

[USB function controller programming reference](/windows-hardware/drivers/ddi/usbfnbase)（USB 功能控制器编程参考）

## <a name="related-topics"></a>相关主题

[Windows 对 USB 类型 C 连接器的支持](oem-tasks-for-bringing-up-a-usb-typec.md)