---
title: 使用设备安装函数
description: 使用设备安装函数
ms.assetid: a7cfa359-a45c-45fa-a854-ee70de66b12e
keywords:
- Setupapi.log 函数 WDK，设备安装功能
- 设备安装功能 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d6289918cefa761d974fa1e5260d03aeb620095
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104090"
---
# <a name="using-device-installation-functions"></a>使用设备安装函数





本部分概述了 [设备安装功能](/previous-versions/ff541299(v=vs.85))。 通过使用设备安装功能，安装软件可以执行以下类型的操作：

-   安装驱动程序

-   处理 DIF 代码。

-   管理设备信息集。

-   管理驱动程序列表。

-   管理设备接口。

-   管理图标和其他位图。

若要执行本部分中所述的 Setupapi.log 函数不支持的设备安装操作，请调用相应的 [常规设置函数](/previous-versions/ff544985(v=vs.85)) 或 [PnP Configuration Manager 函数](/previous-versions/ff549717(v=vs.85)) (CM_*Xxx* 函数<em>) 。</em>

下表提供了以下类型的函数的摘要：

[驱动程序安装功能](#ddk-update-driver-function-dg)

[设备信息函数](#ddk-setupdi-device-information-functions-dg)

[驱动程序信息函数](#ddk-setupdi-driver-information-functions-dg)

[驱动程序选择函数](#ddk-setupdi-driver-selection-functions-dg)

[设备安装处理程序](#ddk-setupdi-device-installation-handlers-dg)

[设备安装自定义功能](#ddk-setupdi-device-installation-customization-functions-dg)

[安装程序类函数](#ddk-setupdi-setup-class-functions-dg)

[位图和图标函数](#ddk-setupdi-class-bitmap-and-icon-functions-dg)

[设备接口函数](#ddk-setupdi-device-interface-functions-dg)

[Windows Vista 和更高版本 (设备属性函数) ](#ddk-setupdi-device-property-functions-dg)

[注册表函数](#ddk-setupdi-registry-functions-dg)

[<c0 />其他函数<c1 />](#ddk-other-setupdi-functions-dg)

### <a name="driver-installation-functions"></a><a href="" id="ddk-update-driver-function-dg"></a>驱动程序安装功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/newdev/nf-newdev-diinstalldevice" data-raw-source="[&lt;strong&gt;DiInstallDevice&lt;/strong&gt;](/windows/desktop/api/newdev/nf-newdev-diinstalldevice)"><strong>DiInstallDevice</strong></a></p></td>
<td align="left"><p>在系统中存在的 PnP 设备上安装 <a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">驱动程序存储区</a> 中预安装的指定驱动程序。  (windows Vista 和更高版本的 Windows) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/newdev/nf-newdev-diinstalldrivera" data-raw-source="[&lt;strong&gt;DiInstallDriver&lt;/strong&gt;](/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)"><strong>DiInstallDriver</strong></a></p></td>
<td align="left"><p>预安装驱动程序存储区中的驱动程序，然后在与系统中存在的匹配 PnP 设备上安装驱动程序。  (windows Vista 和更高版本的 Windows) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/newdev/nf-newdev-dirollbackdriver" data-raw-source="[&lt;strong&gt;DiRollbackDriver&lt;/strong&gt;](/windows/desktop/api/newdev/nf-newdev-dirollbackdriver)"><strong>DiRollbackDriver</strong></a></p></td>
<td align="left"><p>将安装在指定设备上的驱动程序回滚到设备的备份驱动程序集。  (windows Vista 和更高版本的 Windows) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/newdev/nf-newdev-dishowupdatedevice" data-raw-source="[&lt;strong&gt;DiShowUpdateDevice&lt;/strong&gt;](/windows/desktop/api/newdev/nf-newdev-dishowupdatedevice)"><strong>DiShowUpdateDevice</strong></a></p></td>
<td align="left"><p>显示指定设备的硬件更新向导。  (windows Vista 和更高版本的 Windows) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/newdev/nf-newdev-diuninstalldevice" data-raw-source="[&lt;strong&gt;DiUninstallDevice&lt;/strong&gt;](/windows/desktop/api/newdev/nf-newdev-diuninstalldevice)"><strong>DiUninstallDevice</strong></a></p></td>
<td align="left"><p>卸载设备并从系统中删除其设备节点 (<a href="/windows-hardware/drivers/#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>) ) 。 Windows 7 和更高版本的 Windows)  (</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/install/installselecteddriver" data-raw-source="[&lt;strong&gt;InstallSelectedDriver&lt;/strong&gt;](./installselecteddriver.md)"><strong>InstallSelectedDriver</strong></a></p></td>
<td align="left"><p>在选定设备上安装选定的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa" data-raw-source="[&lt;strong&gt;UpdateDriverForPlugAndPlayDevices&lt;/strong&gt;](/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)"><strong>UpdateDriverForPlugAndPlayDevices</strong></a></p></td>
<td align="left"><p>更新为匹配系统中存在的 PnP 设备安装的功能驱动程序。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-information-functions"></a><a href="" id="ddk-setupdi-device-information-functions-dg"></a>设备信息函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist)"><strong>SetupDiCreateDeviceInfoList</strong></a></p></td>
<td align="left"><p>创建空 <a href="device-information-sets.md" data-raw-source="[device information set](device-information-sets.md)">设备信息集</a>。 此集可以与类 GUID 相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolistexa" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoListEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolistexa)"><strong>SetupDiCreateDeviceInfoListEx</strong></a></p></td>
<td align="left"><p>创建空设备信息集。 此集可以与类 GUID 相关联，并且可以用于远程计算机上的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)"><strong>SetupDiCreateDeviceInfo</strong></a></p></td>
<td align="left"><p>创建新的设备信息元素，并将其作为新成员添加到指定的设备信息集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)"><strong>SetupDiOpenDeviceInfo</strong></a></p></td>
<td align="left"><p>检索有关现有设备实例的信息，并将其添加到指定的设备信息集中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)"><strong>SetupDiEnumDeviceInfo</strong></a></p></td>
<td align="left"><p>返回设备信息集的设备信息元素的上下文结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstanceId&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)"><strong>SetupDiGetDeviceInstanceId</strong></a></p></td>
<td align="left"><p>检索与设备信息元素关联的设备实例 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistclass" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListClass&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistclass)"><strong>SetupDiGetDeviceInfoListClass</strong></a></p></td>
<td align="left"><p>如果具有关联的类，则检索与设备信息集关联的类 GUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistdetaila" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListDetail&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistdetaila)"><strong>SetupDiGetDeviceInfoListDetail</strong></a></p></td>
<td align="left"><p>检索与设备信息集关联的信息，包括类 GUID、远程计算机句柄和远程计算机名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevpropertysheetsa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevPropertySheets&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevpropertysheetsa)"><strong>SetupDiGetClassDevPropertySheets</strong></a></p></td>
<td align="left"><p>检索指定设备信息元素的属性表或指定设备信息集的 <a href="/windows-hardware/drivers/install/overview-of-device-setup-classes" data-raw-source="[device setup class](./overview-of-device-setup-classes.md)">设备安装程序类</a> 的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>返回一个设备信息集，其中包含指定类的所有设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>返回一个设备信息集，其中包含本地或远程计算机上指定类的所有设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddevice" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddevice)"><strong>SetupDiSetSelectedDevice</strong></a></p></td>
<td align="left"><p>将指定的设备信息元素设置为设备信息集的当前选定成员。 此函数通常由安装向导使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddevice" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddevice)"><strong>SetupDiGetSelectedDevice</strong></a></p></td>
<td align="left"><p>为指定的设备信息集检索当前选定的设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>使用即插即用管理器注册新创建的设备实例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinfo)"><strong>SetupDiDeleteDeviceInfo</strong></a></p></td>
<td align="left"><p>删除指定设备信息集中的成员。 此函数不会删除实际设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist" data-raw-source="[&lt;strong&gt;SetupDiDestroyDeviceInfoList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist)"><strong>SetupDiDestroyDeviceInfoList</strong></a></p></td>
<td align="left"><p>销毁设备信息集并释放所有关联的内存。</p></td>
</tr>
</tbody>
</table>

 

### <a name="driver-information-functions"></a><a href="" id="ddk-setupdi-driver-information-functions-dg"></a>驱动程序信息函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist" data-raw-source="[&lt;strong&gt;SetupDiBuildDriverInfoList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)"><strong>SetupDiBuildDriverInfoList</strong></a></p></td>
<td align="left"><p>生成与指定设备实例或设备信息集的全局类驱动程序列表相关联的驱动程序列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa" data-raw-source="[&lt;strong&gt;SetupDiEnumDriverInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)"><strong>SetupDiEnumDriverInfo</strong></a></p></td>
<td align="left"><p>枚举驱动程序信息列表的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInfoDetail&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila)"><strong>SetupDiGetDriverInfoDetail</strong></a></p></td>
<td align="left"><p>检索指定驱动程序信息元素的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDriver&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)"><strong>SetupDiSetSelectedDriver</strong></a></p></td>
<td align="left"><p>将驱动程序列表的指定成员设置为当前选择的驱动程序。 它还可以用于重置驱动程序列表，以便当前没有选定的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddrivera" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDriver&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddrivera)"><strong>SetupDiGetSelectedDriver</strong></a></p></td>
<td align="left"><p>检索选作要安装的驱动程序的驱动程序列表的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicanceldriverinfosearch" data-raw-source="[&lt;strong&gt;SetupDiCancelDriverInfoSearch&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicanceldriverinfosearch)"><strong>SetupDiCancelDriverInfoSearch</strong></a></p></td>
<td align="left"><p>取消当前在其他线程中进行的驱动程序列表搜索。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydriverinfolist" data-raw-source="[&lt;strong&gt;SetupDiDestroyDriverInfoList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydriverinfolist)"><strong>SetupDiDestroyDriverInfoList</strong></a></p></td>
<td align="left"><p>销毁驱动程序信息列表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="driver-selection-functions"></a><a href="" id="ddk-setupdi-driver-selection-functions-dg"></a>驱动程序选择函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiaskforoemdisk" data-raw-source="[&lt;strong&gt;SetupDiAskForOEMDisk&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiaskforoemdisk)"><strong>SetupDiAskForOEMDisk</strong></a></p></td>
<td align="left"><p>显示一个对话框，要求用户提供 OEM 安装磁盘的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiselectoemdrv" data-raw-source="[&lt;strong&gt;SetupDiSelectOEMDrv&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectoemdrv)"><strong>SetupDiSelectOEMDrv</strong></a></p></td>
<td align="left"><p>使用用户提供的 OEM 路径选择设备驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 请求的默认处理程序。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-installation-handlers"></a><a href="" id="ddk-setupdi-device-installation-handlers-dg"></a>设备安装处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller" data-raw-source="[&lt;strong&gt;SetupDiCallClassInstaller&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)"><strong>SetupDiCallClassInstaller</strong></a></p></td>
<td align="left"><p>通过指定的安装请求，调用相应的类安装程序和任何已注册的共同安装程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate" data-raw-source="[&lt;strong&gt;SetupDiChangeState&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)"><strong>SetupDiChangeState</strong></a></p></td>
<td align="left"><p>DIF_PROPERTYCHANGE 请求的默认处理程序。 它可用于更改已安装设备的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers" data-raw-source="[&lt;strong&gt;SetupDiRegisterCoDeviceInstallers&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers)"><strong>SetupDiRegisterCoDeviceInstallers</strong></a></p></td>
<td align="left"><p>为指定设备注册 INF 文件中列出的特定于设备的共同安装程序。 此函数是 DIF_REGISTER_COINSTALLERS 的默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice" data-raw-source="[&lt;strong&gt;SetupDiInstallDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)"><strong>SetupDiInstallDevice</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICE 请求的默认处理程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles" data-raw-source="[&lt;strong&gt;SetupDiInstallDriverFiles&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)"><strong>SetupDiInstallDriverFiles</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICEFILES 请求的默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>DIF_INSTALLINTERFACES 请求的默认处理程序。 它将安装 <em>DDInstall</em>中列出的接口。设备 INF 文件的<strong>接口</strong> 部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/install/setupdimoveduplicatedevice" data-raw-source="[&lt;strong&gt;SetupDiMoveDuplicateDevice&lt;/strong&gt;](./setupdimoveduplicatedevice.md)"><strong>SetupDiMoveDuplicateDevice</strong></a></p></td>
<td align="left"><p>此函数已过时，不能在任何 Microsoft Windows 版本中使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice" data-raw-source="[&lt;strong&gt;SetupDiRemoveDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)"><strong>SetupDiRemoveDevice</strong></a></p></td>
<td align="left"><p>DIF_REMOVEDEVICE 请求的默认处理程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice" data-raw-source="[&lt;strong&gt;SetupDiUnremoveDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)"><strong>SetupDiUnremoveDevice</strong></a></p></td>
<td align="left"><p>DIF_UNREMOVE 请求的默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>DIF_REGISTERDEVICE 请求的默认处理程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 请求的默认处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv" data-raw-source="[&lt;strong&gt;SetupDiSelectBestCompatDrv&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)"><strong>SetupDiSelectBestCompatDrv</strong></a></p></td>
<td align="left"><p>DIF_SELECTBESTCOMPATDRV 请求的默认处理程序。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-installation-customization-functions"></a><a href="" id="ddk-setupdi-device-installation-customization-functions-dg"></a>设备安装自定义功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiGetClassInstallParams&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa)"><strong>SetupDiGetClassInstallParams</strong></a></p></td>
<td align="left"><p>检索设备信息集或特定设备信息元素的类安装参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiSetClassInstallParams&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa)"><strong>SetupDiSetClassInstallParams</strong></a></p></td>
<td align="left"><p>设置或清除设备信息集或特定设备信息元素的类安装参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstallParams&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa)"><strong>SetupDiGetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>检索设备信息集或特定设备信息元素的设备安装参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInstallParams&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)"><strong>SetupDiSetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>设置设备信息集或特定设备信息元素的设备安装参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInstallParams&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)"><strong>SetupDiGetDriverInstallParams</strong></a></p></td>
<td align="left"><p>检索指定驱动程序的安装参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiSetDriverInstallParams&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa)"><strong>SetupDiSetDriverInstallParams</strong></a></p></td>
<td align="left"><p>设置指定驱动程序的安装参数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="setup-class-functions"></a><a href="" id="ddk-setupdi-setup-class-functions-dg"></a>安装程序类函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolist" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolist)"><strong>SetupDiBuildClassInfoList</strong></a></p></td>
<td align="left"><p>返回包含系统中安装的每个类的安装程序类 Guid 的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoListEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa)"><strong>SetupDiBuildClassInfoListEx</strong></a></p></td>
<td align="left"><p>返回安装程序类 Guid 的列表，其中包括在本地系统或远程系统上安装的每个类。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescription&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona)"><strong>SetupDiGetClassDescription</strong></a></p></td>
<td align="left"><p>检索与指定安装程序类 GUID 关联的类说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescriptionEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa)"><strong>SetupDiGetClassDescriptionEx</strong></a></p></td>
<td align="left"><p>检索安装在本地或远程计算机上的安装程序类的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetinfclassa" data-raw-source="[&lt;strong&gt;SetupDiGetINFClass&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetinfclassa)"><strong>SetupDiGetINFClass</strong></a></p></td>
<td align="left"><p>检索指定设备 INF 文件的类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnamea" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromName&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnamea)"><strong>SetupDiClassGuidsFromName</strong></a></p></td>
<td align="left"><p>检索与指定类名称关联的 Guid。 此列表基于系统上当前安装的类生成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnameexa" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromNameEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnameexa)"><strong>SetupDiClassGuidsFromNameEx</strong></a></p></td>
<td align="left"><p>检索与指定类名称关联的 Guid。 此结果列表包含本地或远程计算机上当前安装的类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuid&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)"><strong>SetupDiClassNameFromGuid</strong></a></p></td>
<td align="left"><p>检索与类 GUID 关联的类名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguidexa" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuidEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguidexa)"><strong>SetupDiClassNameFromGuidEx</strong></a></p></td>
<td align="left"><p>检索与类 GUID 关联的类名称。 可以在本地或远程计算机上安装类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa" data-raw-source="[&lt;strong&gt;SetupDiInstallClass&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa)"><strong>SetupDiInstallClass</strong></a></p></td>
<td align="left"><p>安装指定 INF 文件的 <strong>ClassInstall32</strong> 节。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>安装类安装程序或接口类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>打开 <a href="/windows-hardware/drivers/install/overview-of-device-setup-classes" data-raw-source="[device setup class](./overview-of-device-setup-classes.md)">设备安装程序类</a> 注册表项或类的特定子项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>打开设备安装程序类注册表项、设备接口类注册表项或类的特定子项。 此函数打开本地计算机或远程计算机上的指定密钥。</p></td>
</tr>
</tbody>
</table>

 

### <a name="bitmap-and-icon-functions"></a><a href="" id="ddk-setupdi-class-bitmap-and-icon-functions-dg"></a>位图和图标函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelist" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelist)"><strong>SetupDiGetClassImageList</strong></a></p></td>
<td align="left"><p>生成一个图像列表，其中包含每个已安装类的位图并返回数据结构中的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelistexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageListEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelistexa)"><strong>SetupDiGetClassImageListEx</strong></a></p></td>
<td align="left"><p>为本地或远程计算机上安装的每个类生成位图的图像列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimageindex" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageIndex&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimageindex)"><strong>SetupDiGetClassImageIndex</strong></a></p></td>
<td align="left"><p>检索指定类的类图像列表中的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassbitmapindex" data-raw-source="[&lt;strong&gt;SetupDiGetClassBitmapIndex&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassbitmapindex)"><strong>SetupDiGetClassBitmapIndex</strong></a></p></td>
<td align="left"><p>检索为指定类提供的迷你图标的索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon" data-raw-source="[&lt;strong&gt;SetupDiDrawMiniIcon&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)"><strong>SetupDiDrawMiniIcon</strong></a></p></td>
<td align="left"><p>在请求的位置绘制指定的小图标。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon" data-raw-source="[&lt;strong&gt;SetupDiLoadClassIcon&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)"><strong>SetupDiLoadClassIcon</strong></a></p></td>
<td align="left"><p>加载指定类的大图标和小图标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiloaddeviceicon" data-raw-source="[&lt;strong&gt;SetupDiLoadDeviceIcon&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiloaddeviceicon)"><strong>SetupDiLoadDeviceIcon</strong></a></p></td>
<td align="left"><p>为指定的设备加载设备图标。  (windows Vista 和更高版本的 Windows) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdidestroyclassimagelist" data-raw-source="[&lt;strong&gt;SetupDiDestroyClassImageList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdidestroyclassimagelist)"><strong>SetupDiDestroyClassImageList</strong></a></p></td>
<td align="left"><p>销毁类图像列表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-interface-functions"></a><a href="" id="ddk-setupdi-device-interface-functions-dg"></a>设备接口函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterface&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea)"><strong>SetupDiCreateDeviceInterface</strong></a></p></td>
<td align="left"><p> (设备) 设备接口注册设备功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterface&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea)"><strong>SetupDiOpenDeviceInterface</strong></a></p></td>
<td align="left"><p>检索有关现有设备接口的信息，并将其添加到指定的设备信息集中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacealias" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceAlias&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacealias)"><strong>SetupDiGetDeviceInterfaceAlias</strong></a></p></td>
<td align="left"><p>返回指定设备接口的别名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>返回一个设备信息集，其中包含指定类的所有设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>返回一个设备信息集，其中包含本地或远程计算机上指定类的所有设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInterfaces&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)"><strong>SetupDiEnumDeviceInterfaces</strong></a></p></td>
<td align="left"><p>返回设备信息集的设备接口元素的上下文结构。 每个调用都将返回有关一个设备接口的信息。</p>
<p>可以重复调用此函数，以获取有关一个或多个设备公开的几个接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceDetail&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)"><strong>SetupDiGetDeviceInterfaceDetail</strong></a></p></td>
<td align="left"><p>返回有关特定设备接口的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>创建注册表子项以存储有关设备接口实例的信息，并返回密钥的句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>打开应用程序和驱动程序使用的注册表子项，以存储特定于设备接口实例的信息，并返回密钥的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>删除应用程序和驱动程序使用的注册表子项，以存储特定于设备接口实例的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>是 DIF_INSTALLINTERFACES 请求的默认处理程序。 它将安装 <em>DDInstall</em>中列出的接口。设备 INF 文件的<strong>接口</strong> 部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedeviceinterface" data-raw-source="[&lt;strong&gt;SetupDiRemoveDeviceInterface&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedeviceinterface)"><strong>SetupDiRemoveDeviceInterface</strong></a></p></td>
<td align="left"><p>从系统中删除已注册的设备接口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfacedata" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceData&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfacedata)"><strong>SetupDiDeleteDeviceInterfaceData</strong></a></p></td>
<td align="left"><p>从设备信息集中删除设备接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacedefault" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceDefault&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacedefault)"><strong>SetupDiSetDeviceInterfaceDefault</strong></a></p></td>
<td align="left"><p>将指定的设备接口设置为设备类的默认接口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>安装类安装程序或接口类。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>打开 <a href="/windows-hardware/drivers/install/overview-of-device-setup-classes" data-raw-source="[device setup class](./overview-of-device-setup-classes.md)">设备安装程序类</a> 注册表项、设备接口类注册表项或类的特定子项。 此函数打开本地计算机或远程计算机上的指定密钥。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-property-functions-windows-vista-and-later"></a><a href="" id="ddk-setupdi-device-property-functions-dg"></a>Windows Vista 和更高版本 (设备属性函数) 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw" data-raw-source="[&lt;strong&gt;SetupDiGetClassProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)"><strong>SetupDiGetClassProperty</strong></a></p></td>
<td align="left"><p>检索为设备安装程序类或设备接口类设置的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)"><strong>SetupDiGetClassPropertyEx</strong></a></p></td>
<td align="left"><p>为本地或远程计算机上的设备安装程序类或设备接口类检索类属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeys&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)"><strong>SetupDiGetClassPropertyKeys</strong></a></p></td>
<td align="left"><p>检索设备属性键的数组，该数组表示为设备安装程序类或设备接口类设置的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeysEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw)"><strong>SetupDiGetClassPropertyKeysEx</strong></a></p></td>
<td align="left"><p>检索设备属性键的数组，该数组表示为本地或远程计算机上的设备安装程序类或设备接口类设置的设备属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)"><strong>SetupDiGetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>检索为设备接口设置的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfacePropertyKeys&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)"><strong>SetupDiGetDeviceInterfacePropertyKeys</strong></a></p></td>
<td align="left"><p>检索表示为设备接口设置的设备属性的设备属性键的数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)"><strong>SetupDiGetDeviceProperty</strong></a></p></td>
<td align="left"><p>检索设备实例属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys" data-raw-source="[&lt;strong&gt;SetupDiGetDevicePropertyKeys&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)"><strong>SetupDiGetDevicePropertyKeys</strong></a></p></td>
<td align="left"><p>检索表示为设备实例设置的设备属性的设备属性键的数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw" data-raw-source="[&lt;strong&gt;SetupDiSetClassProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)"><strong>SetupDiSetClassProperty</strong></a></p></td>
<td align="left"><p>为设备安装程序类或设备接口类设置类属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw" data-raw-source="[&lt;strong&gt;SetupDiSetClassPropertyEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)"><strong>SetupDiSetClassPropertyEx</strong></a></p></td>
<td align="left"><p>为本地或远程计算机上的设备安装程序类或设备接口类设置设备属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)"><strong>SetupDiSetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>设置设备接口的设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)"><strong>SetupDiSetDeviceProperty</strong></a></p></td>
<td align="left"><p>设置设备实例属性。</p></td>
</tr>
</tbody>
</table>

 

### <a name="registry-functions"></a><a href="" id="ddk-setupdi-registry-functions-dg"></a>注册表函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya" data-raw-source="[&lt;strong&gt;SetupDiCreateDevRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)"><strong>SetupDiCreateDevRegKey</strong></a></p></td>
<td align="left"><p>为特定于设备的配置信息创建注册表存储密钥，并返回密钥的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenDevRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)"><strong>SetupDiOpenDevRegKey</strong></a></p></td>
<td align="left"><p>打开注册表存储密钥以获取特定于设备的配置信息，并返回密钥的句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdideletedevregkey" data-raw-source="[&lt;strong&gt;SetupDiDeleteDevRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdideletedevregkey)"><strong>SetupDiDeleteDevRegKey</strong></a></p></td>
<td align="left"><p>删除与设备信息元素关联的指定用户可访问注册表项 (s) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>打开安装程序类的注册表项或类的特定子项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>打开设备安装程序类注册表项、设备接口类注册表项或类的特定子项。</p>
<p>此函数打开本地计算机或远程计算机上的指定密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>创建一个非易失性注册表子项，用于存储有关设备接口实例的信息，并返回该密钥的句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>打开应用程序和驱动程序使用的注册表子项，以存储特定于设备接口实例的信息，并返回密钥的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>删除应用程序和驱动程序使用的注册表子项，以存储特定于设备接口实例的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceRegistryProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)"><strong>SetupDiSetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>设置指定的即插即用设备属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceRegistryProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)"><strong>SetupDiGetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>检索指定即插即用设备属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiGetClassRegistryProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)"><strong>SetupDiGetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>从注册表中检索指定的设备类属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiSetClassRegistryProperty&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)"><strong>SetupDiSetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>在注册表中设置指定的设备类属性。</p></td>
</tr>
</tbody>
</table>

 

### <a name="other-functions"></a><a href="" id="ddk-other-setupdi-functions-dg"></a>其他函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualmodelssectiona" data-raw-source="[&lt;strong&gt;SetupDiGetActualModelsSection&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualmodelssectiona)"><strong>SetupDiGetActualModelsSection</strong></a></p></td>
<td align="left"><p>检索在从设备 INF 文件中安装设备时要使用的相应修饰的 <a href="inf-models-section.md" data-raw-source="[&lt;strong&gt;INF Models section&lt;/strong&gt;](inf-models-section.md)"><strong>INF 模型部分</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstalla" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstall&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstalla)"><strong>SetupDiGetActualSectionToInstall</strong></a></p></td>
<td align="left"><p>检索设备 INF 文件中安装设备时要使用的相应 <em>DDInstall</em> 部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstallexa" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstallEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstallexa)"><strong>SetupDiGetActualSectionToInstallEx</strong></a></p></td>
<td align="left"><p>检索为指定操作系统和处理器体系结构安装设备的 INF <em>DDInstall</em> 部分的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynamea" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyName&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynamea)"><strong>SetupDiGetHwProfileFriendlyName</strong></a></p></td>
<td align="left"><p>检索与硬件配置文件 ID 关联的友好名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynameexa" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyNameEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynameexa)"><strong>SetupDiGetHwProfileFriendlyNameEx</strong></a></p></td>
<td align="left"><p>检索与本地或远程计算机上的硬件配置文件 ID 关联的友好名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelist" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelist)"><strong>SetupDiGetHwProfileList</strong></a></p></td>
<td align="left"><p>检索当前定义的所有硬件配置文件 Id 的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelistexa" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileListEx&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelistexa)"><strong>SetupDiGetHwProfileListEx</strong></a></p></td>
<td align="left"><p>检索本地或远程计算机上当前定义的所有硬件配置文件 Id 的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdirestartdevices" data-raw-source="[&lt;strong&gt;SetupDiRestartDevices&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdirestartdevices)"><strong>SetupDiRestartDevices</strong></a></p></td>
<td align="left"><p>重新启动指定的设备，或者在必要时启动由同一功能操作的所有设备，并筛选驱动程序作为指定设备。</p></td>
</tr>
</tbody>
</table>

 

