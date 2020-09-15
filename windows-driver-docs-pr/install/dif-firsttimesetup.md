---
title: DIF_FIRSTTIMESETUP
description: DIF_FIRSTTIMESETUP
ms.assetid: 6ac4da58-3f4f-4fcd-96e2-c480975159e0
keywords:
- DIF_FIRSTTIMESETUP 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_FIRSTTIMESETUP
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 09213577c0c645d103fad05de5bbc808b77a13ad
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102982"
---
# <a name="dif_firsttimesetup"></a>DIF_FIRSTTIMESETUP


此 DIF 代码保留供系统使用。 供应商提供的安装程序不得处理此请求，除非供应商提供必须由安装程序检测到的非 PnP 设备。

DIF_FIRSTTIMESETUP 请求指示安装程序执行任何特定于类的安装任务，这些任务必须在操作系统的初始安装过程中完成。

### <a name="when-sent"></a>发送时间

GUI 模式安装过程中。

### <a name="who-handles"></a>谁处理

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>类共同安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="even">
<td align="left"><p>设备共同安装程序</p></td>
<td align="left"><p>不处理</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>安装程序输入

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供设备信息集的句柄。 存在与*DeviceInfoSet*关联的[设备安装程序类](./overview-of-device-setup-classes.md)。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
无

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoSet*关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
对于要安装的每个检测到的设备，安装程序将设备信息元素添加到 *DeviceInfoSet* 中。 安装程序还可以生成全局类驱动程序列表。

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改 *DeviceInfoSet* 的设备安装参数，也可以修改它所创建的新设备信息元素的设备安装参数。

### <a name="installer-return-value"></a>安装程序返回值

类共同安装程序可以在预处理或后处理期间检测设备。 此类共同安装程序返回 ERROR_DI_POSTPROCESSING_REQUIRED (，用于后处理) 和/或在其检测操作后返回 NO_ERROR 或 Win32 错误代码。 如果共同安装程序未检测到设备，它将从其预处理传递返回 NO_ERROR。

如果类安装程序检测到设备，安装程序将返回 NO_ERROR 或适当的 Win32 错误代码。 如果类安装程序不处理此 DIF 请求，则安装程序将返回 ERROR_DI_DO_DEFAULT。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

若要在 GUI 模式安装过程中检测非 PnP 设备，安装程序必须处理 DIF_FIRSTTIMESETUP 请求。 GUI 模式安装程序不会向安装程序发送 [**DIF_DETECT**](dif-detect.md) 请求。

GUI 模式安装程序发送一个 DIF_FIRSTTIMESETUP 请求，其中包含空的 *DeviceInfoSet*。 安装程序可以对非 PnP 设备执行旧式检测，并将其添加到 *DeviceInfoSet*中。 系统提供的安装程序还可以在将旧式设备安装从 Windows 9x/Me 或 Windows NT 迁移到 Microsoft Windows 2000 及更高版本的 Windows 时处理此 DIF 请求。

安装程序会根据注册表信息、通过调用内核模式检测组件来检测其安装程序类的新设备，或通过咨询 *unattend.txt* 在操作系统升级过程中运行迁移 DLL 时存储的信息。

如果安装程序检测到非 PnP 设备，则安装程序应为设备选择驱动程序，如下所示：创建设备信息元素 ([**SetupDiCreateDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)) ，通过调用 [**SetupDiSetDeviceRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)设置 SPDRP_HARDWAREID 属性，调用 [**SetupDiBuildDriverInfoList**](/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)，然后调用 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 发送 [**DIF_SELECTBESTCOMPATDRV**](dif-selectbestcompatdrv.md) 请求。

如果一个或多个安装程序检测到设备 (s) 以响应此 DIF 代码，GUI 模式安装程序将尝试安装 () 的设备。 GUI 模式安装程序将尝试安装列表中的所有设备;如果安装程序返回先前配置的设备，GUI 模式安装程序将安装两次设备。

安装程序必须以无提示方式处理此 DIF 请求。 也就是说，不向用户显示 UI。

如果安装程序处理需要重新启动计算机的此 DIF 请求，则不应执行任务。 例如，在下一次启动时，类安装程序不应将驱动程序设置为加载，目的是在重新启动后确定哪些驱动程序成功。

若要在 GUI 模式安装过程中检测非 PnP 设备，安装程序必须处理此请求。 GUI 模式安装程序不发送 DIF_DETECT 请求。

有关 DIF 代码的详细信息，请参阅 [处理 Dif 代码](./handling-dif-codes.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.log (包含 Setupapi.log) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DIF_SELECTBESTCOMPATDRV**](dif-selectbestcompatdrv.md)

[**SetupDiBuildDriverInfoList**](/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)

[**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)

[**SetupDiCreateDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)

[**SetupDiSetDeviceRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

 

