---
title: USB 的特定于设备的方法 (_DSM)
description: 若要支持 USB 子系统的设备类特定配置，Windows 定义特定于设备的方法 (_DSM) 具有本文中介绍的函数。
ms.assetid: 8F0EDE17-9895-4C24-B061-963DA0D7882B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cda503d75207e5e8ac1fa152af9b8f456466849
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353946"
---
# <a name="usb-device-specific-method-dsm"></a>USB 设备特定的方法 (\_DSM)


若要支持 USB 子系统的设备类特定配置，Windows 定义了特定于设备的方法 (\_DSM) 已在本文中介绍的函数。

## <a name="function-1-post-reset-processing-for-dual-role-controllers"></a>函数 1:对于双角色控制器处理后重置


\_DSM 控制后重置处理函数的方法参数的双角色 USB 控制器，如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = ce2ee385-00e6-48cb-9f05-2edb927c4899
-   **Arg1:** 修订 ID = 0
-   **Arg2:** 函数索引 = 1
-   **Arg3:** （未使用） 的空包

### <a name="return"></a>返回

无 Windows 收件箱驱动程序仅支持在主机模式下的 USB 控制器。 USB 驱动程序的每个控制器重置后，将调用\_DSM 函数索引 1，以执行任何配置 USB 控制器在主机模式下操作所需的特定于控制器的初始化。

使用此函数时， \_DSM 方法必须出现在 USB 控制器设备下。

## <a name="function-2-port-type-identification"></a>函数 2:端口类型标识


\_DSM 控件方法参数用于标识 USB 端口类型如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = ce2ee385-00e6-48cb-9f05-2edb927c4899
-   **Arg1:** 修订 ID = 0
-   **Arg2:** 函数索引 = 2
-   **Arg3:** （未使用） 的空包

### <a name="return"></a>返回

一个整数，它包含以下值之一：

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
<td>整数 （字节）</td>
<td><p>指定 USB 端口的类型：</p>
<ul>
<li>0x00 – 常规 USB</li>
<li>0X01-HSIC</li>
<li>0x02 – SSIC</li>
<li>0x03-0xff 保留</li>
</ul></td>
</tr>
</tbody>
</table>

 

使用此函数时， \_DSM 方法必须出现在 USB 端口设备下。

**请注意**  函数索引为 0 的每个\_DSM 是返回集支持的函数的索引，并始终是必需的查询函数。 有关详细信息，请参阅部分 9.14.1，"\_DSM （设备特定的方法）"，在[ACPI 5.0 规范](https://uefi.org/specifications)。

 

 

 




