---
title: 处理 DIF 代码
description: 处理 DIF 代码
ms.assetid: cb54bc04-4cd4-4eec-ad74-2abbf601de54
keywords:
- 共同安装程序 WDK 设备安装，DIF 代码
- DIF 代码 WDK 设备安装
- 设备安装函数代码 WDK
- 函数代码 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 546430989db1e5f3f6389a3a17faf55aa776869b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386290"
---
# <a name="handling-dif-codes"></a>处理 DIF 代码





*设备安装应用程序*发送[设备安装函数代码](https://msdn.microsoft.com/library/windows/hardware/ff541307)（DIF 代码） 安装程序通过调用[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922). 此函数中，依次调用安装程序的入口点函数。 安装程序入口点的说明，请参阅：

[共同安装程序界面](co-installer-interface.md)

每个差异代码的参考页包含以下部分：

<a href="" id="when-sent"></a>**发送时**  
介绍了典型的时间时，以及为什么，设备安装应用程序将发送此 DIF 请求的原因。

<a href="" id="who-handles"></a>**谁处理**  
指定允许的安装程序来处理此请求。 安装程序包括类安装程序、 类共同安装程序 （安装程序类范围共同安装程序），以及设备共同安装程序 （特定于设备的共同安装程序）。

<a href="" id="installer-input"></a>**安装程序输入**  
DIF 代码中，除了**SetupDiCallClassInstaller**提供与特定请求相关的其他信息。 使用每个请求提供的信息，请参阅有关详细信息的每个差异代码的参考页。 以下列表包含额外的输入参数的一般描述，并列出[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)(**SetupDi * Xxx*** 函数) 的安装程序可以调用来处理参数：

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供的句柄的设备信息设置。

不透明句柄。 使用该句柄，例如，若要识别设备信息设置在调用**SetupDi * Xxx*** 函数。

*DeviceInfoSet*可能有一个关联[设备安装程序类](device-setup-classes.md)。 如果是这样，调用[ **SetupDiGetDeviceInfoListClass** ](https://msdn.microsoft.com/library/windows/hardware/ff551101)若要获取的类 GUID。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
根据需要提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)标识的设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>*设备安装参数*   
这些间接参数提供有关中的设备安装信息[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构。 如果*DeviceInfoData*不是**NULL**，有设备与关联的安装参数*DeviceInfoData*。 如果*DeviceInfoData*是**NULL**，与之关联的设备安装参数*DeviceInfoSet*。

调用[ **SetupDiGetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551104)若要获取设备的安装参数。

<a href="" id="class-installation-parameters"></a>*类的安装参数*  
可选的间接参数是特定于特定 DIF 请求。 这些是实质上是"DIF 请求参数。" 例如，SP_REMOVEDEVICE_PARAMS 结构中包含 DIF_REMOVE 安装请求的类安装参数。

每个 SP_*XXX*_PARAMS 结构启动具有固定大小 SP_CLASSINSTALL_HEADER 结构。

调用[ **SetupDiGetClassInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551083)获取类安装参数。

如果差异请求具有类安装参数，则与关联的参数集*DeviceInfoSet*另一组相关联的参数*DeviceInfoData* （如果 DIF 请求指定*DeviceInfoData*)。 **SetupDiGetClassInstallParams**返回可用的最特定参数。

<a href="" id="context"></a>*上下文*  
共同安装程序具有的可选上下文参数。

<a href="" id="installer-output"></a>**安装程序输出**  
介绍此 DIF 代码预期的输出。

如果安装程序修改了设备安装参数，安装程序必须调用[ **SetupDiSetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552141)返回之前应用所做的更改。 同样，如果安装程序修改 DIF 代码类安装参数，则安装程序必须调用[ **SetupDiSetClassInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff552122)。

<a href="" id="installer-return-value"></a>**安装程序返回值**  
指定适当的返回值的差异代码。 请参阅下图，了解有关返回值的详细信息。

<a href="" id="default-dif-code-handler"></a>**默认 DIF 代码处理程序**  
指定**SetupDi * Xxx*** DIF 代码的系统定义的默认操作将执行的函数。 并非所有 DIF 代码都有默认处理程序。 辅助安装程序或类的安装程序不需要步骤防止默认处理程序被调用，除非**SetupDiCallClassInstaller** DIF 代码调用默认处理程序，它会调用类安装程序之后 （但在调用任何之前共同安装程序为后续处理注册）。

如果类安装程序已成功处理 DIF 代码和**SetupDiCallClassInstaller**应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序能够成功处理 DIF 代码，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。 请注意，类安装程序可以直接调用默认处理程序，但应永远不会尝试类安装程序来取代默认处理程序的操作。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

共同安装程序应*不*调用 DIF 代码处理程序的默认值。

<a href="" id="installer-operation"></a>**安装程序操作**  
介绍了安装程序可能用来处理 DIF 请求的典型步骤。

<a href="" id="see-also"></a>**另请参阅**  
列出了相关信息的源。

下图显示了中的事件序列**SetupDiCallClassInstaller**处理 DIF 代码。

![说明在 setupdicallclassinstaller 中处理 dif 代码流的关系图](images/dif-flow.png)

操作系统执行某些操作为每个差异代码。 供应商提供共同安装程序和类安装程序可以参与的安装活动。 请注意， **SetupDiCallClassInstaller**调用注册的共同安装程序的后续处理即使 DIF 代码失败。

 

 





