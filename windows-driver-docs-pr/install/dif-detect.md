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
ms.openlocfilehash: a26c57dd7f444ad87f49240f4b73a1a4f2d33594
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354658"
---
# <a name="difdetect"></a>DIF_DETECT


DIF_DETECT 请求指示安装程序检测特定类的非 PnP 设备并将设备添加到设备的信息集。 此请求用于非 PnP 设备。

### <a name="when-sent"></a>发送时间

当**添加硬件向导**检测非 PnP 设备。

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
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)。 没有[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)与关联*DeviceInfoSet*。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
无

<a href="" id="device-installation-parameters-"></a>设备安装参数   
没有设备与关联的安装参数*DeviceInfoSet*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_DETECTDEVICE_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)与关联结构*DeviceInfoSet*。 参数包含类安装程序调用以指示检测操作的进度的回调例程。

### <a name="installer-output"></a>安装程序输出

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
安装程序将添加到的设备信息元素*DeviceInfoSet*为每个设备检测到，而不考虑以前检测到并安装设备。

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改的设备安装参数*DeviceInfoSet*或为其创建的新设备信息元素。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不会检测设备，则返回 NO_ERROR 从其预处理阶段。 如果共同安装程序检测到设备，它可以在预处理或后处理过程中执行此操作，并返回 NO_ERROR 或 Win32 错误代码。

如果类安装程序检测到设备，则返回 NO_ERROR 或相应的 Win32 错误代码。 如果类安装程序不处理此 DIF 请求，则返回 ERROR_DI_DO_DEFAULT。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

在对 DIF_DETECT 请求响应安装程序可检测设备及其安装程序类。

如果安装程序检测到设备，它应执行至少以下操作：

-   调用**DetectProgressNotify**中的回调例程[ **SP_DETECTDEVICE_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)类的安装参数，如果检测可能会出现明显时间量。

-   对于每个安装程序检测到的设备，它应当：
    -   创建设备信息元素 ([**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa))。
    -   提供有关驱动程序选项的信息。

        安装程序手动选择该设备驱动程序或安装程序可以设置设备的硬件 ID，Windows 将用来查找设备 INF。 安装程序通过调用来设置的硬件 ID [ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)与*属性*SPDRP_HARDWAREID 的值。

    -   可能将某些设备设置安装参数。

-   为成功检测返回 NO_ERROR 或返回一个 Win32 错误代码。

如果一个或多个安装程序检测到对此 DIF 代码的响应中的设备，Windows 将检测到的设备到设备的当前列表的列表进行比较。 如果安装程序检测到新设备，Windows 将尝试安装该设备。 如果安装程序忽略设备安装程序的列表中出现，Windows 通常会删除设备。

若要在 GUI 模式下安装过程中检测到非 PnP 设备，安装程序必须处理[ **DIF_FIRSTTIMESETUP** ](dif-firsttimesetup.md)请求。 GUI 模式下安装程序不向安装程序发送 DIF_DETECT 请求。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Microsoft Windows 2000 和更高版本的 Windows 支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DIF_DETECT**](dif-detect.md)

[**DIF_FIRSTTIMESETUP**](dif-firsttimesetup.md)

[**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)

[**SP_DETECTDEVICE_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






