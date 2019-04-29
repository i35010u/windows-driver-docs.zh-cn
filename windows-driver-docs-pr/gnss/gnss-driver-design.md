---
title: GNSS 驱动程序设计
description: 讨论开发包括数据结构、 错误报告和驱动程序版本控制的 Windows 10 GNSS 驱动程序时要考虑的设计原则。
ms.assetid: E10B1149-CC8B-438D-B537-258F7FCFA0E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b473f66d65a4bb251272f149a5b7110f57de3b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371123"
---
# <a name="gnss-driver-design"></a>GNSS 驱动程序设计


讨论开发包括数据结构、 错误报告和驱动程序版本控制的 Windows 10 GNSS 驱动程序时要考虑的设计原则。

## <a name="data-structures"></a>数据结构


有关向后兼容性和将来的扩展，所有数据结构都开始使用版本号和大小以适应将来的扩展和向后兼容性问题。 作为额外的保护，每个结构还具有要保留静态结构大小相同，即使新字段都将添加填充缓冲区。 这是为了防止错误地使用结构的静态编译时大小的任何较旧 GNSS 驱动程序 (使用**sizeof**) 而不是结构的动态大小。

除非另行指定，所有参数将都遵循单位国际系统 (SI):

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th>单位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>距离、 阈值或级别</p></td>
<td><p><strong>meter</strong></p></td>
</tr>
<tr class="even">
<td><p>超时值或间隔</p></td>
<td><p><strong>second</strong></p></td>
</tr>
<tr class="odd">
<td><p>速度</p></td>
<td><p><strong>meter/second</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="error-reporting"></a>错误报告


GNSS DDI 期望**NTSTATUS**作为的驱动程序的返回值。 仅成功和失败的情况下在高级别操作系统 (HLOS) 充当基于这些错误消息，不会查找在特定的错误消息。 它仍是首选驱动程序返回紧密映射到相应的错误**NTSTATUS**错误消息。 GNSS 驱动程序可以发送其自己的自定义**NTSTATUS**错误消息都以进行诊断可能会非常有用。

## <a name="driver-versioning"></a>驱动程序版本控制


为 GNSS DDI 指定每个结构包含驱动程序版本字段，而且许多结构包含一个填充字段。 这两个这些组件用来缓解 GNSS DDI，使用以下策略的新版本：

-   框架和驱动程序进行通信使用功能交换过程及其各自的版本。 这些 Ioctl 视为特殊，因为它们通信使用的版本字段及其版本。 因此，关于设备和平台功能检查的实现应显式检查版本返回第一次，并将其存储的使用情况。 版本隶属[ **GNSS\_设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/dn925104)结构进行通信的驱动程序的版本号。 版本隶属[ **GNSS\_平台\_功能**](https://msdn.microsoft.com/library/windows/hardware/dn925205)结构通信 GNSS 适配器的版本号。

-   每当添加新字段时，如果该结构有一个填充字段，空间应退出而不是将添加到结构，它将保持二进制兼容性填充

-   每当添加新字段时，被视为 GNSS DDI 的版本递增。 这将反映在注释中的 GNSS DDI 标头本身，但不是公开为一个常量。 GNSS 适配器和 GNSS 驱动程序将使用专用的常量值以指示其当前版本。 这允许 GNSS 适配器和驱动程序的特定版本进行编码。

-   GNSS 适配器必须与较旧版本 GNSS 驱动程序的向后兼容。 如果协议更改 DDI 的新版本中引入，符合新 GNSS DDI 的 GNSS 适配器必须实现新协议仅适用于新版本的驱动程序，并使用旧的协议进行较旧版本的驱动程序。

-   GNSS 驱动程序必须是向前兼容 GNSS 适配器的较新版本，并且应将 GNSS 适配器的较新版本的功能编码时的当前版本与相同的方式。

-   GNSS 适配器的较旧版本不应正常 GNSS 驱动程序的较新版本。 为了便于 GNSS 适配器和 DDI 的新版本的 GNSS 驱动程序的共同开发，GNSS 适配器以阻止更高版本 GNSS 驱动程序中将存在没有严格版本检查。 但是，实现 DDI 的较新版本的 GNSS 驱动程序不将其发给包含实现对 GNSS DDI 较早版本的 GNSS 适配器的零售设备。

-   不将 GNSS 适配器支持的任何 Windows 8.1 或旧 GNSS 传感器驱动程序。 这些驱动程序将继续通过旧堆栈在 Windows 10 中正常工作。 存在另一个 Windows 10 GNSS 驱动程序的旧 GNSS 传感器驱动程序的使用情况是未定义。

 

 




