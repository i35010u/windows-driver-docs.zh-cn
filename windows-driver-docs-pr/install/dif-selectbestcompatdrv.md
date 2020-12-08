---
title: DIF_SELECTBESTCOMPATDRV
description: DIF_SELECTBESTCOMPATDRV
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
ms.openlocfilehash: 05f0888cbb680290f3300c3b77eb88789f5073e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799491"
---
# <a name="dif_selectbestcompatdrv"></a>DIF_SELECTBESTCOMPATDRV

> [!NOTE]
> 此请求已在 Windows 10 版本 1703 (Redstone 2) 中弃用。 在最新版本的 Windows 中，不再调用此回调。

DIF_SELECTBESTCOMPATDRV 请求允许安装程序从设备信息元素的兼容驱动程序列表中选择最佳驱动程序。

### <a name="when-sent"></a>发送时间

当操作系统准备安装新的 PnP 设备或在 PnP 设备上执行更改驱动程序操作时。

此 DIF 请求通常在 PnP 配置过程中使用。 如果手动安装了某个设备，Windows 将发送 [**DIF_SELECTDEVICE**](dif-selectdevice.md) 请求。

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
提供包含设备的 [设备信息集](./device-information-sets.md) 的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与 *DeviceInfoData* 关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备安装参数。 但在处理此 DIF 请求时，它们通常不会。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
作为副作用，安装程序可以修改与 *DeviceInfoData* 关联的驱动程序列表，尤其是 SP_DRVINSTALL_PARAMS。

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可以返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序成功处理此请求，并且 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。

**注意**   类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

 

有关调用默认处理程序的详细信息，请参阅 [调用默认的 DIF 代码处理程序](./calling-the-default-dif-code-handlers.md)。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiSelectBestCompatDrv**](/windows/win32/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)

### <a name="installer-operation"></a>安装程序操作

安装程序将处理此 DIF 请求，以便加入为 PnP 设备选择驱动程序。 安装程序通常以下列方式之一响应此 DIF 请求：

-   不执行任何操作。

    如果安装程序没有特殊的选择要求，则不会对此 DIF 请求执行任何操作。 类安装程序返回 ERROR_DI_DO_DEFAULT，共同安装程序 NO_ERROR 返回。

-   修改驱动程序列表中的一个或多个驱动程序的参数。

    例如，安装程序可能会通过将驱动程序标记 DNF_BAD_DRIVER 来删除该设备的驱动程序。 安装程序按以下步骤修改驱动程序参数：

    1.  通过调用 [**SetupDiEnumDriverInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdriverinfoa) 和 [**SetupDiGetDriverInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)获取有关列表中第一个驱动程序的信息。 如果需要，请修改驱动程序参数，并通过调用 [**SetupDiSetDriverInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa)应用该更改。

        如果驱动程序是最坏的选择，请在驱动程序安装参数中将驱动程序的排名设置为0xFFFF 或更高。 查看 [Windows 如何选择驱动程序](./how-windows-selects-a-driver-for-a-device.md) 以获取详细信息。

    2.  重复上述步骤，直到处理完列表中的所有驱动程序。 请确保将 *MemberIndex* 参数递增为 [**SetupDiEnumDriverInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdriverinfoa) ，如该函数的 "引用" 页中所述。

    类安装程序修改了驱动程序列表后，将返回 ERROR_DI_DO_DEFAULT。 如果共同安装程序修改了驱动程序列表，则它应在预处理中执行此操作，并返回 NO_ERROR。

-   选择设备的最佳驱动程序。

    此操作不太常见，但安装程序可能会为设备选择最佳驱动程序。 此类安装程序将检查每个驱动程序的数据，选择一个驱动程序，然后调用 [**SetupDiSetSelectedDriver**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddrivera) 来设置该驱动程序。 安装程序设置选定的驱动程序后，它将返回 NO_ERROR。

    如果共同安装程序选择了驱动程序，则应在后处理时执行此操作。

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


[**SetupDiSelectBestCompatDrv**](/windows/win32/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)

[**SetupDiSetSelectedDriver**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddrivera)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

