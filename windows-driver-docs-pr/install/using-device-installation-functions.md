---
title: 使用设备安装函数
description: 使用设备安装函数
ms.assetid: a7cfa359-a45c-45fa-a854-ee70de66b12e
keywords:
- 安装程序 Api 函数 WDK，设备安装函数
- 设备安装函数 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dbf67fa17ae99a66ea2e7241c2b1d0969daa498
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350408"
---
# <a name="using-device-installation-functions"></a>使用设备安装函数





本部分总结了[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)。 通过使用设备安装功能，安装软件可以执行以下类型的操作：

-   安装驱动程序

-   处理 DIF 代码。

-   管理设备信息设置。

-   管理驱动程序列表。

-   管理设备接口。

-   管理图标和其他位图。

若要执行本部分中描述的安装程序 Api 函数不支持的设备安装操作，调用适当[常规安装函数](https://msdn.microsoft.com/library/windows/hardware/ff544985)或[即插即用 Configuration Manager 功能](https://msdn.microsoft.com/library/windows/hardware/ff549717)(CM_*Xxx*函数<em>)。</em>

下表提供以下类型的函数的摘要：

[驱动程序安装函数](#ddk-update-driver-function-dg)

[设备信息函数](#ddk-setupdi-device-information-functions-dg)

[驱动程序信息函数](#ddk-setupdi-driver-information-functions-dg)

[驱动程序选择函数](#ddk-setupdi-driver-selection-functions-dg)

[设备安装处理程序](#ddk-setupdi-device-installation-handlers-dg)

[设备安装自定义函数](#ddk-setupdi-device-installation-customization-functions-dg)

[安装程序类函数](#ddk-setupdi-setup-class-functions-dg)

[位图和图标函数](#ddk-setupdi-class-bitmap-and-icon-functions-dg)

[设备接口函数](#ddk-setupdi-device-interface-functions-dg)

[设备属性函数 (Windows Vista 及更高版本)](#ddk-setupdi-device-property-functions-dg)

[注册表函数](#ddk-setupdi-registry-functions-dg)

[其他函数](#ddk-other-setupdi-functions-dg)

### <a href="" id="ddk-update-driver-function-dg"></a>驱动程序安装函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544710" data-raw-source="[&lt;strong&gt;DiInstallDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544710)"><strong>DiInstallDevice</strong></a></p></td>
<td align="left"><p>安装指定的驱动程序中已预装<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">驱动程序存储区</a>系统中存在的即插即用设备上。 （Windows Vista 和更高版本的 Windows）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544717" data-raw-source="[&lt;strong&gt;DiInstallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544717)"><strong>DiInstallDriver</strong></a></p></td>
<td align="left"><p>预安装了驱动程序存储区中的驱动程序，然后将匹配的系统中存在的即插即用设备上安装驱动程序。 （Windows Vista 和更高版本的 Windows）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544721" data-raw-source="[&lt;strong&gt;DiRollbackDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544721)"><strong>DiRollbackDriver</strong></a></p></td>
<td align="left"><p>回滚到为设备设置的备份驱动程序在指定设备安装的驱动程序。 （Windows Vista 和更高版本的 Windows）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544727" data-raw-source="[&lt;strong&gt;DiShowUpdateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544727)"><strong>DiShowUpdateDevice</strong></a></p></td>
<td align="left"><p>显示指定设备的硬件更新向导。 （Windows Vista 和更高版本的 Windows）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544754" data-raw-source="[&lt;strong&gt;DiUninstallDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544754)"><strong>DiUninstallDevice</strong></a></p></td>
<td align="left"><p>卸载设备并删除其设备节点 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>)) 从系统。 （Windows 7 和更高版本的 Windows）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547654" data-raw-source="[&lt;strong&gt;InstallSelectedDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547654)"><strong>InstallSelectedDriver</strong></a></p></td>
<td align="left"><p>在所选的设备上安装了所选驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553534" data-raw-source="[&lt;strong&gt;UpdateDriverForPlugAndPlayDevices&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553534)"><strong>UpdateDriverForPlugAndPlayDevices</strong></a></p></td>
<td align="left"><p>更新为匹配的系统中存在的即插即用设备安装的功能驱动程序。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-information-functions-dg"></a>设备信息函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550956" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550956)"><strong>SetupDiCreateDeviceInfoList</strong></a></p></td>
<td align="left"><p>创建一个空<a href="device-information-sets.md" data-raw-source="[device information set](device-information-sets.md)">设备信息集</a>。 此组可以与类 GUID 相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550958" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550958)"><strong>SetupDiCreateDeviceInfoListEx</strong></a></p></td>
<td align="left"><p>创建一个空的设备信息集。 这组类 GUID 与相关联，并且可以是远程计算机上的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550952" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550952)"><strong>SetupDiCreateDeviceInfo</strong></a></p></td>
<td align="left"><p>创建新的设备信息元素并将其作为新成员添加到指定的设备信息设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552071" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552071)"><strong>SetupDiOpenDeviceInfo</strong></a></p></td>
<td align="left"><p>检索有关现有实例的设备信息并将其添加到指定的设备信息设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551010" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551010)"><strong>SetupDiEnumDeviceInfo</strong></a></p></td>
<td align="left"><p>返回设备信息元素的设备信息集的上下文的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551106" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstanceId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551106)"><strong>SetupDiGetDeviceInstanceId</strong></a></p></td>
<td align="left"><p>检索设备信息元素与关联的设备实例 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551101" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListClass&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551101)"><strong>SetupDiGetDeviceInfoListClass</strong></a></p></td>
<td align="left"><p>检索设备信息设置如果它具有一个关联的类关联的 GUID 的类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551103" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListDetail&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551103)"><strong>SetupDiGetDeviceInfoListDetail</strong></a></p></td>
<td align="left"><p>检索设备信息设置包括类 GUID、 远程计算机句柄和远程计算机的名称相关联的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551064" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevPropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551064)"><strong>SetupDiGetClassDevPropertySheets</strong></a></p></td>
<td align="left"><p>检索指向指定的设备信息元素或属性表的句柄<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">设备安装程序类</a>指定的设备信息设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551069" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551069)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>返回包含指定类的所有设备的设备信息集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551072" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551072)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>返回包含指定类的本地或远程计算机上的所有设备的设备信息集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552176" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552176)"><strong>SetupDiSetSelectedDevice</strong></a></p></td>
<td align="left"><p>设置为当前所选的设备信息的成员的指定的设备信息元素集。 安装向导通常使用此函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552011" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552011)"><strong>SetupDiGetSelectedDevice</strong></a></p></td>
<td align="left"><p>检索指定的设备信息设置的当前所选设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552091" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552091)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>在插管理器注册一个新创建的设备实例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550978" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550978)"><strong>SetupDiDeleteDeviceInfo</strong></a></p></td>
<td align="left"><p>从指定的设备信息组中删除成员。 此函数不会删除实际的设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550996" data-raw-source="[&lt;strong&gt;SetupDiDestroyDeviceInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550996)"><strong>SetupDiDestroyDeviceInfoList</strong></a></p></td>
<td align="left"><p>销毁设备信息集并释放所有关联的内存。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-driver-information-functions-dg"></a>驱动程序信息函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550917" data-raw-source="[&lt;strong&gt;SetupDiBuildDriverInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550917)"><strong>SetupDiBuildDriverInfoList</strong></a></p></td>
<td align="left"><p>生成与指定的设备实例或设备信息设置的全局类驱动程序列表关联的驱动程序的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551018" data-raw-source="[&lt;strong&gt;SetupDiEnumDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551018)"><strong>SetupDiEnumDriverInfo</strong></a></p></td>
<td align="left"><p>枚举驱动程序的信息列表中的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551973" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInfoDetail&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551973)"><strong>SetupDiGetDriverInfoDetail</strong></a></p></td>
<td align="left"><p>检索指定的驱动程序信息元素的详细的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552183" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552183)"><strong>SetupDiSetSelectedDriver</strong></a></p></td>
<td align="left"><p>将驱动程序列表的指定的成员设置为当前所选的驱动程序。 此外可以用于重置驱动程序列表，以便任何当前所选驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552013" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552013)"><strong>SetupDiGetSelectedDriver</strong></a></p></td>
<td align="left"><p>检索被选为驱动程序安装的驱动程序列表的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550928" data-raw-source="[&lt;strong&gt;SetupDiCancelDriverInfoSearch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550928)"><strong>SetupDiCancelDriverInfoSearch</strong></a></p></td>
<td align="left"><p>取消当前正在不同线程中的驱动程序列表中搜索。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551001" data-raw-source="[&lt;strong&gt;SetupDiDestroyDriverInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551001)"><strong>SetupDiDestroyDriverInfoList</strong></a></p></td>
<td align="left"><p>销毁驱动程序的信息列表。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-driver-selection-functions-dg"></a>驱动程序选择函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550905" data-raw-source="[&lt;strong&gt;SetupDiAskForOEMDisk&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550905)"><strong>SetupDiAskForOEMDisk</strong></a></p></td>
<td align="left"><p>显示一个对话框，要求用户提供 OEM 安装磁盘的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552121" data-raw-source="[&lt;strong&gt;SetupDiSelectOEMDrv&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552121)"><strong>SetupDiSelectOEMDrv</strong></a></p></td>
<td align="left"><p>选择通过使用 OEM 路径的用户提供的设备的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552115" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552115)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 请求的默认处理程序。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-installation-handlers-dg"></a>设备安装处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550922" data-raw-source="[&lt;strong&gt;SetupDiCallClassInstaller&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550922)"><strong>SetupDiCallClassInstaller</strong></a></p></td>
<td align="left"><p>调用适当的类安装程序，以及任何注册与指定的安装请求的共同安装程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550930" data-raw-source="[&lt;strong&gt;SetupDiChangeState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550930)"><strong>SetupDiChangeState</strong></a></p></td>
<td align="left"><p>DIF_PROPERTYCHANGE 请求默认处理程序。 它可以用于更改已安装的设备的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552085" data-raw-source="[&lt;strong&gt;SetupDiRegisterCoDeviceInstallers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552085)"><strong>SetupDiRegisterCoDeviceInstallers</strong></a></p></td>
<td align="left"><p>注册指定的设备 INF 文件中列出的特定于设备的共同安装程序。 此函数是 DIF_REGISTER_COINSTALLERS 的默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552039" data-raw-source="[&lt;strong&gt;SetupDiInstallDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552039)"><strong>SetupDiInstallDevice</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICE 请求默认处理程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552048" data-raw-source="[&lt;strong&gt;SetupDiInstallDriverFiles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552048)"><strong>SetupDiInstallDriverFiles</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICEFILES 请求默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552043" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552043)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>DIF_INSTALLINTERFACES 请求默认处理程序。 它将安装中列出的接口<em>DDInstall</em>。<strong>接口</strong>设备 INF 文件部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552062" data-raw-source="[&lt;strong&gt;SetupDiMoveDuplicateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552062)"><strong>SetupDiMoveDuplicateDevice</strong></a></p></td>
<td align="left"><p>此函数已过时，不能在任何版本的 Microsoft Windows 中使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552097" data-raw-source="[&lt;strong&gt;SetupDiRemoveDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552097)"><strong>SetupDiRemoveDevice</strong></a></p></td>
<td align="left"><p>DIF_REMOVEDEVICE 请求默认处理程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552193" data-raw-source="[&lt;strong&gt;SetupDiUnremoveDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552193)"><strong>SetupDiUnremoveDevice</strong></a></p></td>
<td align="left"><p>DIF_UNREMOVE 请求默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552091" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552091)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>DIF_REGISTERDEVICE 请求默认处理程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552115" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552115)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 请求默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552112" data-raw-source="[&lt;strong&gt;SetupDiSelectBestCompatDrv&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552112)"><strong>SetupDiSelectBestCompatDrv</strong></a></p></td>
<td align="left"><p>DIF_SELECTBESTCOMPATDRV 请求默认处理程序。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-installation-customization-functions-dg"></a>设备安装自定义函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551083" data-raw-source="[&lt;strong&gt;SetupDiGetClassInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551083)"><strong>SetupDiGetClassInstallParams</strong></a></p></td>
<td align="left"><p>检索设备信息集或特定设备信息元素的类安装参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552122" data-raw-source="[&lt;strong&gt;SetupDiSetClassInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552122)"><strong>SetupDiSetClassInstallParams</strong></a></p></td>
<td align="left"><p>设置或清除的设备信息集或特定设备信息元素的类安装参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551104" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551104)"><strong>SetupDiGetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>检索设备信息集或特定设备信息元素的设备安装参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552141" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552141)"><strong>SetupDiSetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>设置设备的信息集或特定设备信息元素的设备安装参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551978" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551978)"><strong>SetupDiGetDriverInstallParams</strong></a></p></td>
<td align="left"><p>检索安装参数指定的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552172" data-raw-source="[&lt;strong&gt;SetupDiSetDriverInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552172)"><strong>SetupDiSetDriverInstallParams</strong></a></p></td>
<td align="left"><p>设置指定的驱动程序的安装参数。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-setup-class-functions-dg"></a>安装程序类函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550909" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550909)"><strong>SetupDiBuildClassInfoList</strong></a></p></td>
<td align="left"><p>返回安装程序的列表包含在系统上安装的每个类的类 Guid。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550911" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550911)"><strong>SetupDiBuildClassInfoListEx</strong></a></p></td>
<td align="left"><p>返回安装程序的列表包括本地系统或远程系统上安装的每个类的类 Guid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551053" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescription&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551053)"><strong>SetupDiGetClassDescription</strong></a></p></td>
<td align="left"><p>检索与指定的安装程序类 GUID 关联的类说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551058" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescriptionEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551058)"><strong>SetupDiGetClassDescriptionEx</strong></a></p></td>
<td align="left"><p>检索本地或远程计算机上安装的安装程序类的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552010" data-raw-source="[&lt;strong&gt;SetupDiGetINFClass&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552010)"><strong>SetupDiGetINFClass</strong></a></p></td>
<td align="left"><p>检索指定的设备 INF 文件的类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550937" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550937)"><strong>SetupDiClassGuidsFromName</strong></a></p></td>
<td align="left"><p>检索与指定的类名称相关联的 Guid。 此列表是基于生成系统上当前安装哪些类。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550941" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromNameEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550941)"><strong>SetupDiClassGuidsFromNameEx</strong></a></p></td>
<td align="left"><p>检索与指定的类名称相关联的 Guid。 此生成的列表包含当前安装在本地或远程计算机上的类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550947" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550947)"><strong>SetupDiClassNameFromGuid</strong></a></p></td>
<td align="left"><p>检索与类 GUID 关联的类名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550950" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuidEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550950)"><strong>SetupDiClassNameFromGuidEx</strong></a></p></td>
<td align="left"><p>检索与类 GUID 关联的类名称。 类可以安装在本地或远程计算机上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552024" data-raw-source="[&lt;strong&gt;SetupDiInstallClass&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552024)"><strong>SetupDiInstallClass</strong></a></p></td>
<td align="left"><p>将安装<strong>ClassInstall32</strong>部分指定的 INF 文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552032" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552032)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>安装类安装程序或接口类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552065" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552065)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>此时将打开<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">设备安装程序类</a>注册表项或类的特定子项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552067" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552067)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>打开设备安装程序类注册表项、 设备接口的类注册表项或类的特定子项。 此函数将打开指定的键在本地计算机或远程计算机上。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-class-bitmap-and-icon-functions-dg"></a>位图和图标函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551080" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551080)"><strong>SetupDiGetClassImageList</strong></a></p></td>
<td align="left"><p>生成图像列表包含已安装的每个类的位图，并返回一种数据结构中的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551081" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551081)"><strong>SetupDiGetClassImageListEx</strong></a></p></td>
<td align="left"><p>生成本地或远程计算机上安装的每个类的位图图像的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551074" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551074)"><strong>SetupDiGetClassImageIndex</strong></a></p></td>
<td align="left"><p>检索指定类的类图像列表中的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551047" data-raw-source="[&lt;strong&gt;SetupDiGetClassBitmapIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551047)"><strong>SetupDiGetClassBitmapIndex</strong></a></p></td>
<td align="left"><p>检索指定的类提供的最小化图标的索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551005" data-raw-source="[&lt;strong&gt;SetupDiDrawMiniIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551005)"><strong>SetupDiDrawMiniIcon</strong></a></p></td>
<td align="left"><p>在请求的位置绘制指定的最小化图标。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552053" data-raw-source="[&lt;strong&gt;SetupDiLoadClassIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552053)"><strong>SetupDiLoadClassIcon</strong></a></p></td>
<td align="left"><p>加载这两个大和最小化图标为指定的类。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552057" data-raw-source="[&lt;strong&gt;SetupDiLoadDeviceIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552057)"><strong>SetupDiLoadDeviceIcon</strong></a></p></td>
<td align="left"><p>加载指定的设备的设备图标。 （Windows Vista 和更高版本的 Windows）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550995" data-raw-source="[&lt;strong&gt;SetupDiDestroyClassImageList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550995)"><strong>SetupDiDestroyClassImageList</strong></a></p></td>
<td align="left"><p>销毁类图像列表。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-interface-functions-dg"></a>设备接口函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550965" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550965)"><strong>SetupDiCreateDeviceInterface</strong></a></p></td>
<td align="left"><p>注册设备的设备功能 （设备接口）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552074" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552074)"><strong>SetupDiOpenDeviceInterface</strong></a></p></td>
<td align="left"><p>检索有关现有设备接口的信息，并将其添加到指定的设备信息设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551108" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceAlias&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551108)"><strong>SetupDiGetDeviceInterfaceAlias</strong></a></p></td>
<td align="left"><p>返回指定的设备接口的别名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551072" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551072)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>返回包含指定类的所有设备的设备信息集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551072" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551072)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>返回包含指定类的本地或远程计算机上的所有设备的设备信息集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551015" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551015)"><strong>SetupDiEnumDeviceInterfaces</strong></a></p></td>
<td align="left"><p>返回设备信息设置的设备界面元素的上下文结构。 每次调用返回一个设备接口的信息。</p>
<p>可以重复调用该函数，以获取有关多个接口公开一个或多个设备的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551120" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceDetail&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551120)"><strong>SetupDiGetDeviceInterfaceDetail</strong></a></p></td>
<td align="left"><p>返回有关特定设备接口的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550967" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550967)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>创建一个用于存储设备接口实例的信息的注册表子项，并返回的句柄的密钥。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552075" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552075)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>将打开由应用程序和驱动程序来存储特定于设备接口实例，返回的句柄密钥的信息的注册表子项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550986" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550986)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>删除应用程序和驱动程序中用于存储特定于设备接口实例的信息的注册表子项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552043" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552043)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>是 DIF_INSTALLINTERFACES 请求的默认处理程序。 它将安装中列出的接口<em>DDInstall</em>。<strong>接口</strong>设备 INF 文件部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552102" data-raw-source="[&lt;strong&gt;SetupDiRemoveDeviceInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552102)"><strong>SetupDiRemoveDeviceInterface</strong></a></p></td>
<td align="left"><p>从系统中删除已注册的设备接口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550984" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550984)"><strong>SetupDiDeleteDeviceInterfaceData</strong></a></p></td>
<td align="left"><p>从设备信息组中删除设备接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552149" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceDefault&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552149)"><strong>SetupDiSetDeviceInterfaceDefault</strong></a></p></td>
<td align="left"><p>将指定的设备接口设置为设备类的默认接口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552032" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552032)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>安装类安装程序或接口类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552067" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552067)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>此时将打开<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">设备安装程序类</a>注册表项、 设备接口的类注册表项或类的特定子项。 此函数将打开指定的键在本地计算机或远程计算机上。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-property-functions-dg"></a>设备属性函数 (Windows Vista 及更高版本)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551086" data-raw-source="[&lt;strong&gt;SetupDiGetClassProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551086)"><strong>SetupDiGetClassProperty</strong></a></p></td>
<td align="left"><p>检索为设备安装程序类或设备接口类设置的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551090" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551090)"><strong>SetupDiGetClassPropertyEx</strong></a></p></td>
<td align="left"><p>检索设备安装程序类或在本地或远程计算机上的设备接口类的类属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551091" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeys&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551091)"><strong>SetupDiGetClassPropertyKeys</strong></a></p></td>
<td align="left"><p>检索表示为设备安装程序类或设备接口类设置的设备属性的设备属性键的数组。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551093" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeysEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551093)"><strong>SetupDiGetClassPropertyKeysEx</strong></a></p></td>
<td align="left"><p>检索表示为设备安装程序类或设备接口类上本地或远程计算机设置的设备属性的设备属性键的数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551122" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551122)"><strong>SetupDiGetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>检索为设备接口设置的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551959" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfacePropertyKeys&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551959)"><strong>SetupDiGetDeviceInterfacePropertyKeys</strong></a></p></td>
<td align="left"><p>检索表示为设备接口设置的设备属性的设备属性键的数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551963" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551963)"><strong>SetupDiGetDeviceProperty</strong></a></p></td>
<td align="left"><p>检索设备实例属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551965" data-raw-source="[&lt;strong&gt;SetupDiGetDevicePropertyKeys&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551965)"><strong>SetupDiGetDevicePropertyKeys</strong></a></p></td>
<td align="left"><p>检索表示为设备实例设置的设备属性的设备属性键的数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552128" data-raw-source="[&lt;strong&gt;SetupDiSetClassProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552128)"><strong>SetupDiSetClassProperty</strong></a></p></td>
<td align="left"><p>设置设备安装程序类或设备接口类的类属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552132" data-raw-source="[&lt;strong&gt;SetupDiSetClassPropertyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552132)"><strong>SetupDiSetClassPropertyEx</strong></a></p></td>
<td align="left"><p>在本地或远程计算机上设置设备安装程序类或设备接口类的设备的属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552158" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552158)"><strong>SetupDiSetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>设置设备接口的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552163" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552163)"><strong>SetupDiSetDeviceProperty</strong></a></p></td>
<td align="left"><p>设置设备实例属性。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-registry-functions-dg"></a>注册表函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550973" data-raw-source="[&lt;strong&gt;SetupDiCreateDevRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550973)"><strong>SetupDiCreateDevRegKey</strong></a></p></td>
<td align="left"><p>创建特定于设备的配置信息的注册表存储密钥，并返回的句柄的密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552079" data-raw-source="[&lt;strong&gt;SetupDiOpenDevRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552079)"><strong>SetupDiOpenDevRegKey</strong></a></p></td>
<td align="left"><p>打开注册表存储项特定于设备的配置信息并返回一个句柄的键。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550991" data-raw-source="[&lt;strong&gt;SetupDiDeleteDevRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550991)"><strong>SetupDiDeleteDevRegKey</strong></a></p></td>
<td align="left"><p>删除与设备信息元素相关联的指定的用户可访问的注册表密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552065" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552065)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>打开安装程序类注册表项或类的特定子项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552067" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552067)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>打开设备安装程序类注册表项、 设备接口的类注册表项或类的特定子项。</p>
<p>此函数将打开指定的键在本地计算机或远程计算机上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550967" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550967)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>创建一个用于存储设备接口实例的信息的非易失性的注册表子项，并返回的句柄密钥。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552075" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552075)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>将打开由应用程序和驱动程序来存储特定于设备接口实例，返回的句柄密钥的信息的注册表子项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550986" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550986)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>删除应用程序和驱动程序中用于存储特定于设备接口实例的信息的注册表子项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552169" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552169)"><strong>SetupDiSetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>设置指定即插即用设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551967" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551967)"><strong>SetupDiGetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>检索指定即插即用设备属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551097" data-raw-source="[&lt;strong&gt;SetupDiGetClassRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551097)"><strong>SetupDiGetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>从注册表检索指定的设备类属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552135" data-raw-source="[&lt;strong&gt;SetupDiSetClassRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552135)"><strong>SetupDiSetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>在注册表中设置指定的设备类属性。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-other-setupdi-functions-dg"></a>其他函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551029" data-raw-source="[&lt;strong&gt;SetupDiGetActualModelsSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551029)"><strong>SetupDiGetActualModelsSection</strong></a></p></td>
<td align="left"><p>检索相应的修饰<a href="inf-models-section.md" data-raw-source="[&lt;strong&gt;INF Models section&lt;/strong&gt;](inf-models-section.md)"> <strong>INF 模型部分</strong></a>从设备 INF 文件安装设备时要使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551039" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551039)"><strong>SetupDiGetActualSectionToInstall</strong></a></p></td>
<td align="left"><p>检索相应<em>DDInstall</em>从设备 INF 文件安装设备时要使用的部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551045" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstallEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551045)"><strong>SetupDiGetActualSectionToInstallEx</strong></a></p></td>
<td align="left"><p>检索名称 INF <em>DDInstall</em>安装指定的操作系统和处理器体系结构的设备的部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551983" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551983)"><strong>SetupDiGetHwProfileFriendlyName</strong></a></p></td>
<td align="left"><p>检索硬件配置文件 id。 与关联的友好名称</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551989" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyNameEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551989)"><strong>SetupDiGetHwProfileFriendlyNameEx</strong></a></p></td>
<td align="left"><p>检索与本地或远程计算机上的硬件配置文件 ID 关联的友好名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551997" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551997)"><strong>SetupDiGetHwProfileList</strong></a></p></td>
<td align="left"><p>检索所有当前定义的硬件配置文件 Id 的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552006" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552006)"><strong>SetupDiGetHwProfileListEx</strong></a></p></td>
<td align="left"><p>检索本地或远程计算机上的所有当前定义的硬件配置文件 Id 的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552104" data-raw-source="[&lt;strong&gt;SetupDiRestartDevices&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552104)"><strong>SetupDiRestartDevices</strong></a></p></td>
<td align="left"><p>重新启动指定的设备，或如有必要，将启动由同一个函数和筛选器驱动程序为指定的设备操作的所有设备。</p></td>
</tr>
</tbody>
</table>

 

 

 





