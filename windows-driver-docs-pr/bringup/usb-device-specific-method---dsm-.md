---
title: USB 的特定于设备的方法 (_DSM)
description: 为了支持 USB 子系统的设备特定于设备的配置，Windows 定义了一个 Device-Specific 方法 (_DSM 包含本文所述函数的) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5232d4823c316fe3345b55146935c1a5ebfc7554
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809733"
---
# <a name="usb-device-specific-method-_dsm"></a> (DSM) 的 USB Device-Specific 方法 \_


为了支持 USB 子系统的设备特定于设备的配置，Windows 定义了一个 Device-Specific 方法 (\_ DSM) ，其中包含本文所述的函数。

## <a name="function-1-post-reset-processing-for-dual-role-controllers"></a>函数1：双重角色控制器的重置后处理


\_双角色 USB 控制器的重置后处理函数的 DSM 控制方法参数如下：

### <a name="arguments"></a>自变量

-   **Arg0：** UUID = ce2ee385-00e6-48cb-9f05-2edb927c4899
-   **Arg1：** 修订版 ID = 0
-   **Arg2：** 函数 index = 1
-   **Arg3：** 空包 (未使用) 

### <a name="return"></a>返回

无 Windows 收件箱驱动程序仅支持主机模式下的 USB 控制器。 每个控制器重置后，USB 驱动程序将调用 \_ DSM 函数索引1来执行任何特定于控制器的初始化，将 USB 控制器配置为在主机模式下操作。

使用此函数时， \_ DSM 方法必须出现在 USB 控制器设备下。

## <a name="function-2-port-type-identification"></a>函数2：端口类型标识


\_用于标识 USB 端口类型的 DSM 控制方法参数如下：

### <a name="arguments"></a>自变量

-   **Arg0：** UUID = ce2ee385-00e6-48cb-9f05-2edb927c4899
-   **Arg1：** 修订版 ID = 0
-   **Arg2：** 函数 index = 2
-   **Arg3：** 空包 (未使用) 

### <a name="return"></a>返回

一个包含以下值之一的整数：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>对象类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>端口类型</td>
<td>整数 (字节) </td>
<td><p>指定 USB 端口的类型：</p>
<ul>
<li>0x00 –常规 USB</li>
<li>0x01 – HSIC</li>
<li>0x02 – SSIC</li>
<li>0x03 – 0xff reserved</li>
</ul></td>
</tr>
</tbody>
</table>

 

使用此函数时， \_ DSM 方法必须出现在 USB 端口设备下。

**注意**  每个 DSM 的函数索引 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关详细信息，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)中的 9.14.1 "DSM (设备特定方法) " 部分。

 

 

 




