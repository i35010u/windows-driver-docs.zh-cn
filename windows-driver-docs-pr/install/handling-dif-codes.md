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
ms.openlocfilehash: 09349ca33193340989d3d686de9e347c836c5922
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105552"
---
# <a name="handling-dif-codes"></a>处理 DIF 代码





*设备安装应用程序*通过调用[**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)，将[设备安装函数代码](/previous-versions/ff541307(v=vs.85)) (的 DIF 代码发送到安装程序) 。 此函数反过来调用安装程序的入口点函数。 有关安装程序入口点的说明，请参阅：

[辅助安装程序界面](co-installer-interface.md)

每个 DIF 代码的参考页包含以下部分：

<a href="" id="when-sent"></a>**发送时间**  
描述设备安装应用程序发送此 DIF 请求的典型时间和原因。

<a href="" id="who-handles"></a>**谁处理**  
指定允许哪些安装程序处理此请求。 安装程序包括类安装程序、类 (安装程序类的共同安装程序) 和设备共同安装程序 (特定于设备的共同安装程序) 。

<a href="" id="installer-input"></a>**安装程序输入**  
除 DIF 代码外， **SetupDiCallClassInstaller** 还提供与特定请求相关的其他信息。 有关每个请求提供的信息的详细信息，请参阅每个 DIF 代码的参考页。 下面的列表包含对其他输入参数的常规说明，并列出了安装程序可以调用来处理参数) 的 [设备安装函数](/previous-versions/ff541299(v=vs.85)) (**SetupDi * Xxx*** 函数：

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供设备信息集的句柄。

句柄不透明。 例如，使用句柄标识在调用 **SetupDi * Xxx*** 函数时设置的设备信息。

*DeviceInfoSet*可能具有关联的[设备安装程序类](./overview-of-device-setup-classes.md)。 如果是这样，请调用 [**SetupDiGetDeviceInfoListClass**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistclass) 以获取类 GUID。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
还可以提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>*设备安装参数*   
这些间接参数以 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a) 结构提供设备安装的信息。 如果 *DeviceInfoData* 不为 **NULL**，则存在与 *DeviceInfoData*关联的设备安装参数。 如果 *DeviceInfoData* 为 **NULL**，则设备安装参数与 *DeviceInfoSet*相关联。

调用 [**SetupDiGetDeviceInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa) 以获取设备安装参数。

<a href="" id="class-installation-parameters"></a>*类安装参数*  
可选的间接参数专用于特定的 DIF 请求。 它们实质上是 "DIF 请求参数"。 例如，DIF_REMOVE 安装请求的类安装参数包含在 SP_REMOVEDEVICE_PARAMS 结构中。

每个 SP_*XXX*_PARAMS 结构都从固定大小的 SP_CLASSINSTALL_HEADER 结构开始。

调用 [**SetupDiGetClassInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa) 以获取类安装参数。

如果某个 DIF 请求具有类安装参数，则如果该 DIF 请求指定*DeviceInfoData*) ，则会有一组与*DeviceInfoSet*关联的参数，以及与*DeviceInfoData* (关联的另一组参数。 **SetupDiGetClassInstallParams** 返回最具体的可用参数。

<a href="" id="context"></a>*快捷*  
共同安装程序具有一个可选的上下文参数。

<a href="" id="installer-output"></a>**安装程序输出**  
描述此 DIF 代码所需的输出。

如果安装程序修改了设备安装参数，则安装程序必须调用 [**SetupDiSetDeviceInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa) 来应用更改，然后再返回。 同样，如果安装程序修改了 DIF 代码的类安装参数，则安装程序必须调用 [**SetupDiSetClassInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa)。

<a href="" id="installer-return-value"></a>**安装程序返回值**  
为 DIF 代码指定适当的返回值。 有关返回值的详细信息，请参阅下图。

<a href="" id="default-dif-code-handler"></a>**默认的 DIF 代码处理程序**  
指定为 DIF 代码执行系统定义的默认操作的 **SetupDi * Xxx*** 函数。 并非所有的 DIF 代码都有默认的处理程序。 除非共同安装程序或类安装程序将执行一些步骤来阻止调用默认处理程序，否则，在调用 SetupDiCallClassInstaller 类 (安装程序后， **SetupDiCallClassInstaller**将调用该 DIF 代码的默认处理程序，但在调用为后处理) 注册的所有共同安装程序之前。

如果类安装程序成功处理某个 DIF 代码，并且 **SetupDiCallClassInstaller** 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理一个 DIF 代码，包括直接调用默认处理程序，则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。 请注意，类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

共同安装程序 *不* 应调用默认的 DIF 代码处理程序。

<a href="" id="installer-operation"></a>**安装程序操作**  
介绍安装程序处理 DIF 请求可能需要执行的典型步骤。

<a href="" id="see-also"></a>**另请参阅**  
列出相关信息的源。

下图显示了 **SetupDiCallClassInstaller** 中用于处理 DIF 代码的事件的顺序。

![说明 setupdicallclassinstaller 中的 dif 代码处理流的示意图](images/dif-flow.png)

操作系统对每个 DIF 代码执行一些操作。 供应商提供的共同安装程序和类安装程序可参与安装活动。 请注意， **SetupDiCallClassInstaller** 会调用注册为后处理的共同安装程序，即使该 DIF 代码失败也是如此。

 

