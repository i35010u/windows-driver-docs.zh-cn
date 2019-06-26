---
title: DIF_SELECTBESTCOMPATDRV
description: DIF_SELECTBESTCOMPATDRV
ms.assetid: aa10f39f-718b-4160-9cfa-668fb0349156
keywords:
- DIF_SELECTBESTCOMPATDRV 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_SELECTBESTCOMPATDRV
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d5dbddad81dd833e2411d12d55a06bc1ee60df4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386896"
---
# <a name="difselectbestcompatdrv"></a>DIF_SELECTBESTCOMPATDRV

> [!NOTE]
> 在 Windows 10 版本 1703 (Redstone 2) 中已弃用此请求。 在较新版本的 Windows 中，不能再调用此回调。

DIF_SELECTBESTCOMPATDRV 请求可让安装程序选择最适合的驱动程序的设备信息元素兼容的驱动程序列表中。

### <a name="when-sent"></a>发送时间

当操作系统正在准备安装新的即插即用设备，或正在执行的即插即用设备上更改驱动程序操作。

通常在 PnP 配置期间使用此差异请求。 如果手动安装设备时，Windows 会发送[ **DIF_SELECTDEVICE** ](dif-selectdevice.md)请求。

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
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备的安装参数。 但是，它们通常消失得不处理此 DIF 请求时。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
产生了负面影响，安装程序可以修改与关联的驱动程序列表*DeviceInfoData*，特别是，SP_DRVINSTALL_PARAMS。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiSelectBestCompatDrv**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)

### <a name="installer-operation"></a>安装程序操作

安装程序将处理此 DIF 请求参与选择即插即用设备的驱动程序。 安装程序通常通过以下方式之一响应此 DIF 请求：

-   不执行任何操作。

    如果安装程序没有任何特殊选择要求，它会在对此 DIF 请求响应中为 nothing。 类安装程序将返回 ERROR_DI_DO_DEFAULT 并共同安装程序返回 NO_ERROR。

-   修改驱动程序列表中的一个或多个驱动程序的参数。

    例如，安装程序可能会删除驱动程序的设备中不考虑通过将其标记 DNF_BAD_DRIVER。 安装程序通过执行以下步骤来修改驱动程序参数：

    1.  获取列表中的第一个驱动程序有关的信息，通过调用[ **SetupDiEnumDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)并[ **SetupDiGetDriverInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa). 如果需要，修改驱动程序参数并将更改应用通过调用[ **SetupDiSetDriverInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa)。

        如果驱动程序是最糟糕的选择，驱动程序的等级为到 0xFFFF 或更高版本中设置驱动程序安装参数。 请参阅[Windows 中如何选择驱动程序](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)有关详细信息。

    2.  重复上一步，直到处理完所有驱动程序列表中。 请确保您递增*MemberIndex*参数[ **SetupDiEnumDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)该函数的参考页中所述。

    类安装程序修改了驱动程序列表后，它将返回 ERROR_DI_DO_DEFAULT。 如果共同安装程序修改驱动程序列表，它应预处理中执行此操作，并返回 NO_ERROR。

-   选择设备的最佳驱动程序。

    此操作并不常见，但是安装程序可能选择该设备的最佳驱动程序。 此类安装程序将检查每个驱动程序数据、 选择的驱动程序，并调用[ **SetupDiSetSelectedDriver** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)设置驱动程序。 安装程序将设置所选驱动程序后，它将返回 NO_ERROR。

    如果共同安装程序选择一个驱动程序，它应实现中后续处理。

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


[**SetupDiSelectBestCompatDrv**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)

[**SetupDiSetSelectedDriver**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






