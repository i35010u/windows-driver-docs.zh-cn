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
ms.openlocfilehash: a0e76a73484167adf1f17d9a027bd694430dc6d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365944"
---
# <a name="difselectdevice"></a>DIF_SELECTDEVICE


DIF_SELECTDEVICE 请求可让参与选择设备驱动程序的安装程序。

### <a name="when-sent"></a>发送时间

在选择新枚举设备的驱动程序或现有的设备 （更改驱动程序） 的新驱动程序。 例如，当用户选择添加/删除硬件并选择调制解调器类。 或者，用户插入的即插即用设备并在发现新硬件向导中选择"选择驱动程序从列表"。

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
提供的句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含为其选择一个驱动程序的设备。 没有[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)与关联*DeviceInfoSet*。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
根据需要提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)标识设备中设备的信息集的结构。

如果*DeviceInfoData*是**NULL**，此请求是要选择的驱动程序[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)与关联*DeviceInfoSet*。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
如果*DeviceInfoData*不是**NULL**，设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与相关联*DeviceInfoData*。 如果*DeviceInfoData*是**NULL**，有设备与关联的安装参数*DeviceInfoSet*。

特别有趣的是**DriverPath**，其中包含 INF(s) 生成驱动程序列表时要使用的位置。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_SELECTDEVICE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553326)与关联结构*DeviceInfoData*如果*DeviceInfoData*不是**NULL**。 否则，类安装参数作为一个整体设置的设备信息相关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备的安装参数。 但是，它不应修改**DriverPath**字段。

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可以修改[ **SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326)。 例如，安装程序可能会指定一个标题和/或 Windows 以使用对话框，要求用户选择的驱动程序中的说明。

如果安装程序将设置新选择设备参数，而不是修改参数设置的上一安装程序中，则安装程序必须为零不设置的字段。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不执行任何操作此 DIF 代码，则返回 NO_ERROR 从其预处理阶段。 如果共同安装程序可处理此 DIF 代码，它应执行存在其预处理中传递，并且返回 NO_ERROR 或 Win32 错误代码。 为后续处理调用共同安装程序时，该驱动程序已选定。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://msdn.microsoft.com/library/windows/hardware/ff537868)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

如果类安装程序将返回 ERROR_DI_BAD_PATH **DriverPath**的相应成员[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构是否不等于**NULL**，但在指定的路径位置的任何有效的驱动程序。 如果在路径位置没有驱动程序或驱动程序，是否可以发生这种情况，但**标志**的成员[ **SP_DRVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553290)设置的每个驱动程序结构与 DN_BAD_DRIVER 标志。 此错误代码的响应，Windows 向用户显示错误。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiSelectDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552115)

### <a name="installer-operation"></a>安装程序操作

在对 DIF_SELECTDEVICE 请求的响应，安装程序执行其设备或设备类，除了默认处理程序的用途所需的任何选择操作。 安装程序通常通过以下方式之一响应此 DIF 请求：

-   不执行任何操作。

    如果安装程序没有任何特殊选择要求，它会在响应此 DIF 代码中为 nothing。 类安装程序将返回 ERROR_DI_DO_DEFAULT 并共同安装程序返回 NO_ERROR。

-   提供 Windows 将显示所选内容 UI 中的 select 字符串。

    安装程序可以提供 select 字符串中的类安装参数 ([**SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326))。 例如，可以修改安装程序**说明**或窗口标头**标题**。

    如果共同安装程序已提供 select 字符串，类安装程序不应提供 select 字符串。 辅助安装程序可能具有更多相关信息。

    如果安装程序修改[ **SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326)，安装程序还必须设置 DI_USECI_SELECTSTRINGS 标志[ **SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346).

    如果安装程序已成功提供了 select 字符串，Windows 仍必须调用默认处理程序。 因此，在这种情况下，辅助安装程序返回 NO_ERROR 和类安装程序将返回 ERROR_DI_DO_DEFAULT。

-   修改设备的安装参数。

    安装程序可以修改设备的安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346))。 例如，安装程序可能会设置 DI_SHOWOEM 标志可使 Windows 显示**从磁盘安装**按钮。

    如果类安装程序已成功修改了设备安装参数，类安装程序将返回 ERROR_DI_DO_DEFAULT。

-   修改用户可以从中选择的驱动程序的列表。

    此操作是否小于常见，但可能的。 修改驱动程序的安装程序列表可能或可能不是，还提供 select 字符串。

    通常修改驱动程序列表中的安装程序将标记不适用于设备的驱动程序。 安装程序将标记标志 DNF_BAD_DRIVER 具有此类驱动程序。 Windows 将忽略这些驱动程序从其向用户显示的列表。

    安装程序将错误的驱动程序标记通过执行以下步骤：

    1.  通过调用生成驱动程序列表[ **SetupDiBuildDriverInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550917)与*DriverType* SPDIT_CLASSDRIVER。
    2.  获取列表中的第一个驱动程序有关的信息，通过调用[ **SetupDiEnumDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551018)并[ **SetupDiGetDriverInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551978). 如果不适合于设备驱动程序，则设置 DNF_BAD_DRIVER 标志**标志**参数的字段。 将更改应用于参数，通过调用[ **SetupDiSetDriverInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff552172)。
    3.  重复上一步，直到处理完所有驱动程序列表中。 请确保您递增*MemberIndex*参数**SetupDiEnumDriverInfo**该函数的参考页中所述。

    安装程序可能将 DNF_BAD_DRIVER 标志设置为一个或多个驱动程序在驱动程序列表中，但安装程序必须清除该标志。

    如果一个或多个安装程序已成功修改驱动程序列表中，Windows 仍然必须调用默认处理程序。 因此，在这种情况下，辅助安装程序返回 NO_ERROR 和类安装程序将返回 ERROR_DI_DO_DEFAULT。

-   显示其自己的驱动程序选择用户界面和设置所选驱动程序。

    仅安装程序类可以显示其自己驱动程序选择的用户界面;共同安装程序不能。 例如，类安装程序可能会显示图片而不是文本列表。

    如果类安装程序已成功设置所选驱动程序，类安装程序将返回 NO_ERROR 和 Windows 不会调用默认处理程序，因此不会显示默认选择界面。

如果在设备的安装参数，设置了 DI_ENUMSINGLEINF 标志**DriverPath**是一个 INF 文件而不是目录的路径的路径。 安装程序必须使用只该单个 INF 生成驱动程序列表。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://msdn.microsoft.com/library/windows/hardware/ff546094)。

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


[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SetupDiSelectDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552115)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326)

 

 






