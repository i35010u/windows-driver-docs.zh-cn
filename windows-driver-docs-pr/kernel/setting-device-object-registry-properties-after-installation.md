---
title: 安装后设置设备对象注册表属性
description: 安装后设置设备对象注册表属性
ms.assetid: e9415497-f61e-49ba-9376-9255e51e72a8
keywords:
- 设备对象 WDK 内核注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b5b81f71b3e2a2827aad3581cb6e596a11bd5d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360280"
---
# <a name="setting-device-object-registry-properties-after-installation"></a>安装后设置设备对象注册表属性





用户模式程序可以使用[设备安装函数](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))要获取或设置驱动程序的设备对象的属性的注册表设置。 安装软件，通常使用这些函数，但它们可由任何用户模式计划。 （该程序必须执行由具有管理员访问权限的用户。）

[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)并[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)函数获取和设置的注册表项每个指定的属性。 *属性*参数指定要获取或设置的属性。 *PropertyBuffer*指向目标缓冲区 （时获取的属性） 或源缓冲区 （时设置的属性） 的属性。

值之间的对应关系*属性*参数和实际的属性如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值为<em>属性</em>参数</th>
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
<td><p>为安全描述符<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_security_descriptor" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_security_descriptor)"> <strong>SECURITY_DESCRIPTOR</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_SECURITY_SDS</p></td>
<td><p>安全描述符的 SDDL 字符串作为</p></td>
</tr>
</tbody>
</table>

 

请注意，提供两种不同方式来获取或设置安全描述符。 您可以指定 SPDRP\_安全值将作为处理安全描述符**安全\_描述符**结构或 SPDRP\_安全\_SDS 将安全性作为一个 SDDL 字符串的描述符。 有关 SDDL 字符串的详细信息，请参阅[设备对象的 SDDL](sddl-for-device-objects.md)。

对于 Windows XP 和更高版本操作系统，程序可以还获取和设置的设备安装程序类的属性值。 使用[ **SetupDiGetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)并[ **SetupDiSetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)函数来获取和设置属性设备安装程序类的值。

有关使用详细信息**SetupDi * Xxx*** 函数，请参阅[使用设备安装函数](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)。

 

 




