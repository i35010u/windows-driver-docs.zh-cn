---
Description: 您需要编写用于连接器的驱动程序如果 USB C 类型系统不包含嵌入式的控制器，否则可加载由 Microsoft 提供 UCSI 驱动程序。
title: 为 USB 类型 C 连接器开发 Windows 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc06240f49b58ce836dbdd86099787314b20ea1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325211"
---
# <a name="developing-windows-drivers-for-usb-type-c-connectors"></a>为 USB 类型 C 连接器开发 Windows 驱动程序
您需要为连接器编写驱动程序，如果您的 USB C 类型系统不实现 PD 状态机，或实现状态机，但不支持通过非 ACPI 传输 UCSI。 如果是这样，您可以加载 Microsoft 提供[UCSI 驱动程序](ucsi.md)。

**目标的受众**

-   USB C 类型系统的驱动程序开发指南不包含嵌入式的控制器。

**上次更新时间**

-   2018 年 9 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

**重要的 Api**

-   [USB 类型 C 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

![“驱动程序”](images/drivers-c.png)


|             硬件/固件功能             |                                                                                                                                                    非可拆分                                                                                                                                                    |                                                                                                                              外接程序卡                                                                                                                               |
|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| USB C 型连接器没有 PD 状态机。 |        [客户端驱动程序写入 UcmTcpciCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-usb-type-c-port-controller-driver)。 <p>使用启动[UcmTcpciCx 端口控制器客户端驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample) </p>        | [客户端驱动程序写入 UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)。 <p>开头[UcmCx 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)。</p> |
|         连接器是 UCSI 符合 ACPI。         |                                                          加载现成驱动程序，UcmUcsiCx.sys 和 UcmUcsiAcpiClient。 请参阅[USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)。                                                           |                                                                                                                                  不可用                                                                                                                                   |
|       连接器是 UCSI 合规而无需 ACPI。        | 写入 UcmUcsiCx 客户端驱动程序。 有关详细信息，请参阅[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)。 <p>开头[此示例模板](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)和 ACPI 部分替换为您所需的总线的实现。 |                                                           [客户端驱动程序写入 UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)。                                                            |
|    具有 PD 状态机，但不是 UCSI 兼容。     |                          [客户端驱动程序写入 UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)。 <p>开头[UcmCx 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)。                          | [客户端驱动程序写入 UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)<p>开头[UcmCx 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)。 </p>  |

## <a name="in-this-section"></a>本节内容
实现到上表中的建议的解决方案阅读这些主题：
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
<td><p>介绍了典型的硬件设计 USB C 类型系统和支持的硬件组件的 Microsoft 提供驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="function-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the function controller on a USB Type-C Windows system](function-controller-bringup-for-a-usb-type-c-system.md)">启动的 USB 类型 C Windows 系统上函数控制器</a></p></td>
<td><p>函数控制器的驱动程序通知有关充电级别操作系统，其 USB C 型连接器支持，并在它可以开始收费和设备可以绘制当前的最长时通知电池子系统。</p></td>
</tr>
<tr class="odd">
<td><p><a href="dual-role-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the dual-role controller for a USB Type-C Windows system](dual-role-controller-bringup-for-a-usb-type-c-system.md)">启动 USB 类型 C Windows 系统双角色控制器</a></p></td>
<td><p>USB 角色切换驱动程序 (URS) 是一套 WDF 类扩展和处理双角色控制器的角色切换功能及其客户端驱动程序。 如果您的系统具有双重角色控制器，则可以切换具体取决于连接到系统的 USB 类型 C 连接器合作伙伴端口设备系统的角色。 这样，如有线停靠感兴趣的情况。</p></td>
</tr>
<tr class="even">
<td><p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">编写 USB 类型 C 连接器驱动程序</a></p></td>
<td><p>介绍管理 USB 类型 C 连接器和连接器驱动程序的预期的行为的 USB 连接器管理器 (UCM)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="write-a-usb-type-c-port-controller-driver.md" data-raw-source="[Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md)">写入 USB 类型 C 端口控制器驱动程序</a></p></td>
<td><p>介绍如何编写与 USB 类型 C 连接器，而无需 PD 状态机进行通信的 USB 类型 C 端口控制器驱动程序。 </p></td>

</tr>
<tr class="even">
<td><p><a href="write-a-ucsi-driver.md" data-raw-source="[Write a UCSI client driver](write-a-ucsi-driver.md)">编写 UCSI 客户端驱动程序</a></p></td>
<td><p>介绍如何使用非 ACPI 传输的 UCSI 符合控制器编写驱动程序。 </p></td>

</tr>

<tr>
<tr class="odd">
<td><a href="policy-manager-client.md" data-raw-source="[Write a USB Type-C Policy Manager client driver](policy-manager-client.md)">编写 USB 类型 C 策略管理器客户端驱动程序</a></td>
<td>提供 Microsoft USB 类型 C 策略管理器监视 USB 类型 C 连接器的活动。 Windows，版本 1809，引入了一组编程接口，可以使用它们编写到策略管理器中的客户端驱动程序。 客户端驱动程序可以参与 USB 类型 C 连接器的策略决策。 此设置后，你可以选择要写入的内核模式导出驱动程序或用户模式驱动程序。 </td>
</tbody>
</table>



**相关的章节**

[写入 USB 角色切换 (URS) 客户端驱动程序 ](usb-dual-role-driver-stack-architecture.md)

[USB dual-role controller driver programming reference](https://msdn.microsoft.com/library/windows/hardware/mt628026)（USB 双角色控制器驱动程序编程参考）

[写入 USB 函数客户端驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  

[USB function controller programming reference](https://msdn.microsoft.com/library/windows/hardware/mt188013)（USB 功能控制器编程参考）

## <a name="related-topics"></a>相关主题

[Windows 支持 USB 类型 C 连接器](oem-tasks-for-bringing-up-a-usb-typec.md)  





