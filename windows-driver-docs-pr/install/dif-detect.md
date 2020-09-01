---
title: DIF_DETECT
description: DIF_DETECT
ms.assetid: 866a99fc-f48e-447d-b5eb-6339dc98d3f2
keywords:
- DIF_DETECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_DETECT
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91dbaeb5b2a0e42429fb91f33219477b2b7d1d3f
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097379"
---
# <a name="dif_detect"></a>DIF_DETECT


DIF_DETECT 请求指示安装程序检测特定类的非 PnP 设备，并将设备添加到设备信息集。 此请求用于非 PnP 设备。

### <a name="when-sent"></a>发送时间

当 **添加硬件向导** 正在检测非 PnP 设备时。

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
提供 [设备信息集](./device-information-sets.md)的句柄。 存在与*DeviceInfoSet*关联的[设备安装程序类](./overview-of-device-setup-classes.md)。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
无

<a href="" id="device-installation-parameters-"></a>设备安装参数   
有与 *DeviceInfoSet*关联的设备安装参数。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_DETECTDEVICE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)结构与*DeviceInfoSet*关联。 参数包含一个回调例程，该类安装程序将调用它来指示检测操作的进度。

### <a name="installer-output"></a>安装程序输出

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
对于检测到的每个设备，安装程序会将设备信息元素添加到 *DeviceInfoSet* ，而不考虑是否检测并安装了某个设备。

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改 *DeviceInfoSet* 的设备安装参数，也可以修改它所创建的新设备信息元素的设备安装参数。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序未检测到设备，它将从其预处理传递返回 NO_ERROR。 如果共同安装程序检测到设备，则可以在预处理或后处理时执行此操作，并返回 NO_ERROR 或 Win32 错误代码。

如果类安装程序检测到设备，它将返回 NO_ERROR 或适当的 Win32 错误代码。 如果类安装程序不处理此 DIF 请求，它将返回 ERROR_DI_DO_DEFAULT。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

为了响应 DIF_DETECT 请求，安装程序可以检测到其安装程序类的设备。

如果安装程序检测到设备，则至少应执行以下操作：

-   如果检测可能会花费很长的时间，请调用[**SP_DETECTDEVICE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)类安装参数中的**DetectProgressNotify**回调例程。

-   对于安装程序检测到的每个设备，应执行以下操作：
    -    ([**SetupDiCreateDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)) 创建设备信息元素。
    -   为驱动程序选择提供信息。

        安装程序可以手动选择设备的驱动程序，或者安装程序可以设置设备的硬件 ID，Windows 将使用该 ID 来查找设备的 INF。 安装程序通过调用*属性*值为 SPDRP_HARDWAREID 的[**SETUPDISETDEVICEREGISTRYPROPERTY**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)设置硬件 ID。

    -   可能设置了一些设备安装参数。

-   返回成功检测的 NO_ERROR 或返回 Win32 错误代码。

如果一个或多个安装程序检测到设备 (s) 以响应此 DIF 代码，Windows 会将检测到的设备的列表与当前设备列表进行比较。 如果安装程序检测到新设备，Windows 将尝试安装该设备。 如果安装程序省略了安装程序列表中显示的设备，则 Windows 通常会删除该设备。

若要在 GUI 模式安装过程中检测非 PnP 设备，安装程序必须处理 [**DIF_FIRSTTIMESETUP**](dif-firsttimesetup.md) 请求。 GUI 模式安装程序不会向安装程序发送 DIF_DETECT 请求。

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

## <a name="see-also"></a>另请参阅


[**DIF_DETECT**](dif-detect.md)

[**DIF_FIRSTTIMESETUP**](dif-firsttimesetup.md)

[**SetupDiCreateDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)

[**SP_DETECTDEVICE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)

[**SP_DEVINSTALL_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

