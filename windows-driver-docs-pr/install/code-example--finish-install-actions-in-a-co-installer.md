---
title: 共同安装程序中的代码示例 Finish-Install 操作
description: 共同安装程序中的代码示例 Finish-Install 操作
keywords:
- 完成-安装操作 WDK 设备安装
- 共同安装程序 WDK 设备安装，完成-安装操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a88e400258ad3f879a430f7b9d8878e12d57afc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827891"
---
# <a name="code-example-finish-install-actions-in-a-co-installer"></a>代码示例：辅助安装程序中的 Finish-Install 操作


在此示例中，共同安装程序将执行以下操作以支持完成安装操作：

-   当共同安装程序收到 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求时，它会调用安装程序提供的函数 *FinishInstallActionsNeeded* ，以确定是否有完成安装操作。  (此示例中未显示 *FinishInstallActionsNeeded* 函数的代码) 。

    如果 *FinishInstallActionsNeeded* 返回 **TRUE**，则共同安装程序将调用 [**SetupDiGetDeviceInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa)来检索设备的设备安装参数，然后调用 [**SetupDiSetDeviceInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)来设置具有 DI_FLAGSEX_FINISHINSTALL_ACTION 标志的设备的 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构的 **FlagsEx** 成员。 通过设置此标志，Windows 将向所有类安装程序、类共同安装程序和安装此设备的设备共同安装程序发送 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求。 此请求将在所有安装操作完成后发送（完成安装操作除外）。

-   当共同安装程序收到 DIF_FINISHINSTALL_ACTION 请求时，共同安装程序将再次调用 *FinishInstallActionsNeeded* ，以确定它是否有完成安装操作，如果是，则执行完成安装操作。 共同安装程序向用户通知完成安装操作正在进行，并等待完成安装操作完成，然后再从处理 DIF_FINISHINSTALL_ACTION 请求。

-   如果完成安装操作成功，则共同安装程序会通知用户已成功完成安装操作。

-   如果完成安装操作需要系统重新启动才能完成完成安装操作，则共同安装程序会调用 SetupDiGetDeviceInstallParams 来检索设备的设备安装参数，然后调用 SetupDiSetDeviceInstallParams 为设备的 **标志** SP_DEVINSTALL_PARAMS 成员设置 DI_NEEDREBOOT 标志。 安装程序还会通知用户需要重新启动系统。

-   如果完成安装操作失败，并且在下次枚举设备时应再次尝试完成安装操作，则共同安装程序会将此情况的用户通知给用户。

    **注意**  从 Windows 8 开始，"完成-安装" 操作只运行一次。 Windows 不会再次自动运行它，特别是在下次枚举设备时不会自动运行，因为这不是在运行时执行的。

     

-   如果完成安装操作失败，并且共同安装程序确定完成安装操作无法成功，则共同安装程序会向用户通知这种情况。

-   默认情况下，如果完成安装操作已成功，则共同安装程序将返回 NO_ERROR 以响应 DIF_FINISHINSTALL_ACTION 请求; 如果完成安装操作失败，并且共同安装程序确定不应再次尝试完成安装操作，则返回。 仅当完成安装操作失败，并且在下一次在管理员上下文中枚举设备时应再次尝试完成安装操作时，共同安装程序才返回 Win32 错误代码。

    **注意**  从 Windows 8 开始，"完成-安装" 操作只运行一次。 Windows 不会再次自动运行它，特别是在下次枚举设备时不会自动运行，因为这不是在运行时执行的。

     

以下共同安装程序代码示例显示了实现完成安装操作的共同安装程序代码的基本结构：

```cpp
DWORD CALLBACK
SampleCoInstaller(
  IN DI_FUNCTION  InstallFunction,
  IN HDEVINFO  DeviceInfoSet,
  IN PSP_DEVINFO_DATA  DeviceInfoData,
  IN OUT PCOINSTALLER_CONTEXT_DATA  Context
  )
{
  SP_DEVINSTALL_PARAMS DeviceInstallParams;
  DWORD ReturnValue = NO_ERROR; // The default return value

  switch(InstallFunction)
  {
    case DIF_NEWDEVICEWIZARD_FINISHINSTALL:
      //
      // Processing for finish-install wizard pages
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
        // should not be attempted again: clean up
        // and notify the user of the failure
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

 

