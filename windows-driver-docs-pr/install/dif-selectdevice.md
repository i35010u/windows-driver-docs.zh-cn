---
title: DIF_SELECTDEVICE
description: DIF_SELECTDEVICE
ms.assetid: c1266182-b88f-406a-876c-e0f15050fdf3
keywords:
- DIF_SELECTDEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_SELECTDEVICE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e7f9d7907f929e1a6e22d37d1ba1750b032adff
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714918"
---
# <a name="dif_selectdevice"></a>DIF_SELECTDEVICE


DIF_SELECTDEVICE 请求允许安装程序选择设备驱动程序。

### <a name="when-sent"></a>发送时间

为新枚举的设备选择驱动程序时，或者为现有设备选择新的驱动程序时 (更改驱动程序) 。 例如，当用户选择 "添加/删除硬件" 并选择调制解调器类时。 或者，用户插入 PnP 设备，并选择 "发现新硬件" 向导中的 "从列表选择驱动程序"。

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
提供 [设备信息集](./device-information-sets.md) 的句柄，其中包含要为其选择驱动程序的设备。 存在与*DeviceInfoSet*关联的[设备安装程序类](./overview-of-device-setup-classes.md)。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
还可以提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

如果*DeviceInfoData*为**NULL**，则此请求将为与*DeviceInfoSet*关联的[设备安装程序类](./overview-of-device-setup-classes.md)选择一个驱动程序。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
如果 *DeviceInfoData* 不为 **NULL**，则 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 与 *DeviceInfoData*关联的设备安装参数 (。 如果 *DeviceInfoData* 为 **NULL**，则存在与 *DeviceInfoSet*关联的设备安装参数。

特别要注意的是 **DriverPath**，其中包含生成驱动程序列表时要使用) INF (的位置。

<a href="" id="class-installation-parameters"></a>类安装参数  
如果*DeviceInfoData*不为**NULL**，则[**SP_SELECTDEVICE_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-_sp_selectdevice_params_a)结构与*DeviceInfoData*关联。 否则，类安装参数将作为一个整体与设备信息集相关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备安装参数。 但是，它不应修改 **DriverPath** 字段。

<a href="" id="class-installation-parameters"></a>类安装参数  
安装程序可以修改 [**SP_SELECTDEVICE_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-_sp_selectdevice_params_a)。 例如，安装程序可能在要求用户选择驱动程序的对话框中指定要使用的 Windows 标题和/或说明。

如果安装程序设置了新的选择设备参数，而不是修改由先前的安装程序设置的参数，则安装程序必须为它未设置的字段零。

### <a name="installer-return-value"></a>安装程序返回值

如果没有对此 DIF 代码执行任何操作，则它将从其预处理传递返回 NO_ERROR。 如果共同安装程序处理此 DIF 代码，则应在其预处理过程中执行此操作，并返回 NO_ERROR 或 Win32 错误代码。 在调用共同安装程序进行后处理时，已选择了驱动程序。

如果类安装程序成功处理此请求，并且 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。

**注意**   类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

 

有关调用默认处理程序的详细信息，请参阅 [调用默认的 DIF 代码处理程序](./calling-the-default-dif-code-handlers.md)。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

如果相应[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构的**DriverPath**成员不等于**NULL**，但指定的路径位置没有有效的驱动程序，则类安装程序将返回 ERROR_DI_BAD_PATH。 如果路径位置没有驱动程序，或者存在驱动程序，但每个驱动程序的[**SP_DRVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-_sp_drvinstall_params)结构的**Flags**成员是通过 DN_BAD_DRIVER 标志设置的，则会发生这种情况。 为了响应此错误代码，Windows 向用户显示错误。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiSelectDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiselectdevice)

### <a name="installer-operation"></a>安装程序操作

为响应 DIF_SELECTDEVICE 请求，安装程序将执行其设备或设备类所需的任何选择操作，而不是默认处理程序执行的操作。 安装程序通常以下列方式之一响应此 DIF 请求：

-   不执行任何操作。

    如果安装程序没有特殊的选择要求，则不会对此 DIF 代码做出任何响应。 类安装程序返回 ERROR_DI_DO_DEFAULT，共同安装程序 NO_ERROR 返回。

-   提供 Windows 将在选择 UI 中显示的选择字符串。

    安装程序可以 ([**SP_SELECTDEVICE_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-_sp_selectdevice_params_a)) 提供类安装参数中的选择字符串。 例如，安装程序可以修改 **说明** 或窗口标题 **标题**。

    如果共同安装程序已提供 select 字符串，类安装程序不应提供 select 字符串。 共同安装程序可能有更多相关信息。

    如果安装程序修改了 [**SP_SELECTDEVICE_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-_sp_selectdevice_params_a)，则安装程序还必须在 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)中设置 DI_USECI_SELECTSTRINGS 标志。

    如果安装程序成功提供 select 字符串，则 Windows 仍必须调用默认处理程序。 因此，在这种情况下，共同安装程序返回 NO_ERROR 并且类安装程序返回 ERROR_DI_DO_DEFAULT。

-   修改设备安装参数。

    安装程序可以 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 修改设备安装参数。 例如，安装程序可能会将 DI_SHOWOEM 标志设置为让 Windows 显示 " **有磁盘** " 按钮。

    如果类安装程序成功修改了设备安装参数，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

-   修改用户可以从中选择的驱动程序列表。

    此操作不太常见，但可能不太常见。 修改驱动程序列表的安装程序可能会（也可能不）提供选择字符串。

    修改驱动程序列表的安装程序通常会将驱动程序 (s 标记) 不适合设备。 安装程序将此类驱动程序标记 DNF_BAD_DRIVER 标志。 Windows 将向用户显示这些驱动程序并将其显示在列表中。

    安装程序通过执行以下步骤来标记错误驱动程序：

    1.  通过使用 SPDIT_CLASSDRIVER 的*DriverType*调用[**SetupDiBuildDriverInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)来生成驱动程序列表。
    2.  通过调用 [**SetupDiEnumDriverInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdriverinfoa) 和 [**SetupDiGetDriverInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)获取有关列表中第一个驱动程序的信息。 如果驱动程序不适合于设备，请在参数的 " **标志** " 字段中设置 DNF_BAD_DRIVER 标志。 通过调用 [**SetupDiSetDriverInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa)将更改应用于参数。
    3.  重复上述步骤，直到处理完列表中的所有驱动程序。 请确保将 *MemberIndex* 参数递增为 **SetupDiEnumDriverInfo** ，如该函数的 "引用" 页中所述。

    安装程序可能会为驱动程序列表中的一个或多个驱动程序设置 DNF_BAD_DRIVER 标志，但安装程序不得清除该标志。

    如果一个或多个安装程序成功修改了驱动程序列表，则 Windows 仍必须调用默认处理程序。 因此，在这种情况下，共同安装程序返回 NO_ERROR 并且类安装程序返回 ERROR_DI_DO_DEFAULT。

-   显示其自己的驱动程序选择用户界面，并设置所选的驱动程序。

    只有类安装程序可以显示其自己的驱动程序选择用户界面;共同安装程序不得。 例如，类安装程序可能会显示图片而不是文本列表。

    如果类安装程序成功设置了选定的驱动程序，则类安装程序将返回 NO_ERROR 并且 Windows 不会调用默认处理程序，因此不会显示默认的选择界面。

如果在设备安装参数中设置 DI_ENUMSINGLEINF 标志，则 **DriverPath** 是单个 INF 文件的路径，而不是目录的路径。 安装程序只能使用单个 INF 来构建驱动程序列表。

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


[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SetupDiSelectDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiselectdevice)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_SELECTDEVICE_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-_sp_selectdevice_params_a)

 

