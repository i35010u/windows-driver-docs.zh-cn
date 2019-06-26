---
title: 类安装程序中的代码示例完成安装操作
description: 类安装程序中的代码示例完成安装操作
ms.assetid: 394f321c-2ce4-4773-b5df-e30ce23b7207
keywords:
- 完成安装操作 WDK 设备安装
- 类安装程序 WDK 设备安装，完成安装操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ac56ce9db3f97e14f54eb424ec624a867a5cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375321"
---
# <a name="code-example-finish-install-actions-in-a-class-installer"></a>代码示例：类安装程序中的 Finish-Install 操作


在此示例中，类安装程序将执行下列操作来支持各种操作，完成安装：

-   当类安装程序收到[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall)请求时，它将调用安装程序提供的函数*FinishInstallActionsNeeded*到确定是否有要执行的完成安装操作。 (有关代码*FinishInstallActionsNeeded*函数未在此示例中显示。)

    如果*FinishInstallActionsNeeded*返回**TRUE**，类安装程序调用[ **SetupDiGetDeviceInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa)检索设备的设备安装参数。 然后，它调用[ **SetupDiSetDeviceInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)若要设置**FlagsEx**隶属[ **SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)设备 DI_FLAGSEX_FINISHINSTALL_ACTION 标志的结构。 设置此标志会导致 Windows 发送[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)到所有类安装程序、 类共同安装程序，并在此安装中涉及的设备共同安装程序的请求设备。 除了完成安装操作已完成，此请求发送后安装的所有操作。

-   当类安装程序收到 DIF_FINISHINSTALL_ACTION 请求时，它将再次调用*FinishInstallActionsNeeded*以确定是否它具有要执行的完成安装操作，并且，如果是这样，将执行完成安装操作。 类安装程序会通知用户完成安装操作是在进度和完成安装操作完成，然后从处理 DIF_FINISHINSTALL_ACTION 请求返回的等待。

-   如果完成安装操作都成功，类安装程序将通知用户已成功完成安装操作。

-   类安装程序完成安装操作所需重启系统以完成完成安装操作，如果调用 SetupDiGetDeviceInstallParams 检索设备的设备安装参数，然后调用若要设置的 SetupDiSetDeviceInstallParams**标志**SP_DEVINSTALL_PARAMS 结构具有 DI_NEEDREBOOT 标志的设备中的成员。 安装程序还通知用户，则需要重新启动系统。

-   如果完成安装操作失败，但应尝试完成安装操作执行下一步枚举设备时，将再次，类安装程序将通知这种情况下的用户。

    **请注意**  开始 Windows 8 中的完成安装操作只运行一次。 Windows 将不再自动运行它，尤其是不是下一步时间设备枚举因为这是未完成安装操作运行时。

     

-   如果完成安装操作失败，而且类安装程序确定曾经无法成功完成安装操作，则类安装程序将通知这种情况下的用户。

-   默认情况下，类安装程序将返回 ERROR_DI_DO_DEFAULT DIF_FINISHINSTALL_ACTION 请求响应中的完成安装操作成功或完成安装操作失败，安装程序确定完成安装操作应不会再次尝试。 安装程序将返回 Win32 错误代码仅在完成安装操作失败并完成安装操作应在下一步中的管理员上下文枚举设备时再试。

    **请注意**  开始 Windows 8 中的完成安装操作只运行一次。 Windows 将不再自动运行它，尤其是不是下一步时间设备枚举因为这是未完成安装操作运行时。

     

以下类安装程序代码示例演示实现完成安装操作的类安装程序代码的基本结构：

```cpp
DWORD CALLBACK
SampleClassInstaller(
  IN DI_FUNCTION  InstallFunction,
  IN HDEVINFO  DeviceInfoSet,
  IN PSP_DEVINFO_DATA  DeviceInfoData,
  )
{
  SP_DEVINSTALL_PARAMS DeviceInstallParams;
  DWORD ReturnValue = ERROR_DI_DO_DEFAULT; // The default return value

  switch(InstallFunction)
  {
    case DIF_NEWDEVICEWIZARD_FINISHINSTALL:
      //
      // Processing for finish-install wizard pages
      // If the class installer has wizard pages,
      // set ReturnValue to NO_ERROR
      //
      // Processing for finish-install actions
      if (FinishInstallActionsNeeded())
      {
        // Obtain the device install parameters for the device
        // and set the DI_FLAGSEX_FINISHINSTALL_ACTION flag
        DeviceInstallParams.cbSize = sizeof(DeviceInstallParams);
        if (SetupDiGetDeviceInstallParams(DeviceInfoSet, DeviceInfoData, &DeviceInstallParams))
        {
          DeviceInstallParams.FlagsEx |= DI_FLAGSEX_FINISHINSTALL_ACTION;
          SetupDiSetDeviceInstallParams(DeviceInfoSet, DeviceInfoData, &DeviceInstallParams);
        }
      }
      break;

    case DIF_FINISHINSTALL_ACTION:
      // Processing for finish-install actions
      if (FinishInstallActionsNeeded())
      {
        //
        // Perform the finish-install actions,
        // notify the user that finish install actions
        // are in progress and wait for
        // the finish-install actions to complete
        //
        // If the finish-install actions succeed, notify the user
        //
        // If the finish install actions require a system restart: 
        // notify the user, call SetupDiGetDeviceInstallParams 
        // to obtain the device install parameters for the device in 
        // DeviceInstallParams, and call SetupDiSetInstallParams to set 
        // the DI_NEEDREBOOT flag in DeviceInstallParams.Flags
        // 
        // If the finish install actions failed, but
        // should be attempted again: clean up,
        // notify the user of the failure, and
        // set ReturnValue to an appropriate Win32 error code
        //
        // If the finish install actions failed and 
        // should not be attempted again: clean up and
        // notify the user of the failure
        //
        // Starting with Windows 8, a finish-install action
        // is only run once. Windows will not automatically
        // run it again, especially not the next time
        // the device is enumerated because that is not when
        // finish-install actions are run.
        //
      }
      break;
  }

  return ReturnValue;
}
```

 

 





