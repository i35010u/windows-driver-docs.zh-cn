---
title: DIF_INSTALLINTERFACES
description: DIF_INSTALLINTERFACES
ms.assetid: fd3eb56b-f73e-4699-accf-6bf70e2e54f8
keywords:
- DIF_INSTALLINTERFACES 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_INSTALLINTERFACES
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a043d19fdcec80d16b2d29aceb423cb1e44ea88a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387046"
---
# <a name="difinstallinterfaces"></a>DIF_INSTALLINTERFACES


DIF_INSTALLINTERFACES 请求可让参与的注册设备的设备接口的安装程序。

### <a name="when-sent"></a>发送时间

注册设备共同安装程序之后、 之前完成设备安装。

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
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>安装程序输入

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可能会修改设备的安装参数，但通常不用于此 DIF 请求。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)

### <a name="installer-operation"></a>安装程序操作

DIF_INSTALLINTERFACES 响应请求安装程序可能注册的设备接口以编程方式而不是通过 INF 文件注册的接口。 通常情况下，供应商提供的安装程序不处理此 DIF 请求。

除非设置了 DI_NOFILECOPY 标志，安装程序以便处理此 DIF 请求应复制所需的设备接口的文件。

如果 DI_NOFILECOPY 标志已清除，但 DI_NOVCP 标志设置，安装程序必须排入队列到队列提供的文件的所有文件操作，但都必须提交队列。

如果安装程序注册了设备接口，必须调用设备 （例如，驱动程序） 的内核模式组件[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)若要启用的界面。

如果安装程序将返回 Win32 错误代码，Windows 将停止安装。

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


[**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






