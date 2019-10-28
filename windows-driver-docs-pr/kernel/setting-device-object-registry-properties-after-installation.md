---
title: 安装后设置设备对象注册表属性
description: 安装后设置设备对象注册表属性
ms.assetid: e9415497-f61e-49ba-9376-9255e51e72a8
keywords:
- 设备对象 WDK 内核，注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 352be178c17be54a1db4faa2d95417fcdc3c9ad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838430"
---
# <a name="setting-device-object-registry-properties-after-installation"></a>安装后设置设备对象注册表属性





用户模式程序可以使用[设备安装功能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))为驱动程序的设备对象的属性获取或设置注册表设置。 通常，这些函数由安装软件使用，但可供任何用户模式程序使用。 （程序必须由具有管理员访问权限的用户执行。）

[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)和[**SetupDiSetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)函数获取并设置每个指定属性的注册表项。 *Property*参数指定要获取或设置的属性。 *PropertyBuffer*指向属性的目标缓冲区（在获取属性时）或源缓冲区（设置属性时）。

*Property*参数的值和实际属性的值之间的对应关系如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><em>Property</em>参数的值</th>
<th>设备对象属性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPDRP_CHARACTERISTICS</p></td>
<td><p>设备特征</p></td>
</tr>
<tr class="even">
<td><p>SPDRP_DEVTYPE</p></td>
<td><p>设备类型</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_EXCLUSIVE</p></td>
<td><p>独占</p></td>
</tr>
<tr class="even">
<td><p>SPDRP_SECURITY</p></td>
<td><p>作为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_security_descriptor" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_security_descriptor)"><strong>SECURITY_DESCRIPTOR</strong></a>结构的安全描述符</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_SECURITY_SDS</p></td>
<td><p>作为 SDDL 字符串的安全描述符</p></td>
</tr>
</tbody>
</table>

 

请注意，提供了两种不同的方法来获取或设置安全描述符。 可以指定 SPDRP\_安全值，将安全描述符视为**安全\_描述符**结构，或指定 SPDRP\_SECURITY\_SDS 将安全描述符视为 SDDL 字符串。 有关 SDDL 字符串的详细信息，请参阅[适用于设备对象的 SDDL](sddl-for-device-objects.md)。

对于 Windows XP 和更高版本的操作系统，程序也可以获取和设置设备安装程序类的属性值。 使用[**SetupDiGetClassRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)和[**SetupDiSetClassRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)函数可获取和设置设备安装程序类的属性值。

有关使用**SetupDi * Xxx*** 函数的详细信息，请参阅[使用设备安装函数](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)。

 

 




