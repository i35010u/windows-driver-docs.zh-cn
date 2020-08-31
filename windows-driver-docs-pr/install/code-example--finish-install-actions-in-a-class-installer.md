---
title: 代码示例完成-在类安装程序中安装操作
description: 代码示例完成-在类安装程序中安装操作
ms.assetid: 394f321c-2ce4-4773-b5df-e30ce23b7207
keywords:
- 完成-安装操作 WDK 设备安装
- 类安装程序 WDK 设备安装，完成-安装操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9300740b52569c664c22c4301e46b2ef8f5feb4
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095163"
---
# <a name="code-example-finish-install-actions-in-a-class-installer"></a>代码示例：类安装程序中的 Finish-Install 操作


在此示例中，类安装程序将执行以下操作以支持完成安装操作：

-   当类安装程序收到 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求时，它会调用安装程序提供的函数 *FinishInstallActionsNeeded* 来确定是否有完成安装操作。  (此示例中未显示 *FinishInstallActionsNeeded* 函数的代码。 ) 

    如果 *FinishInstallActionsNeeded* 返回 **TRUE**，则类安装程序将调用 [**SetupDiGetDeviceInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa) 来检索设备的设备安装参数。 然后，它调用[**SetupDiSetDeviceInstallParams**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)来设置具有 DI_FLAGSEX_FINISHINSTALL_ACTION 标志的设备的[**SP_DEVINSTALL_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)结构的**FlagsEx**成员。 通过设置此标志，Windows 将向所有类安装程序、类共同安装程序和安装此设备的设备共同安装程序发送 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求。 此请求在除完成安装操作完成之外的所有安装操作后发送。

-   当类安装程序收到 DIF_FINISHINSTALL_ACTION 请求时，它会再次调用 *FinishInstallActionsNeeded* 来确定它是否有完成安装操作，如果是，则执行完成安装操作。 类安装程序向用户通知完成安装操作正在进行，并等待完成安装操作完成，然后再从处理 DIF_FINISHINSTALL_ACTION 请求。

-   如果完成安装操作成功，类安装程序将向用户通知完成安装操作是否成功。

-   如果完成安装操作需要重新启动系统才能完成完成安装操作，则类安装程序会调用 SetupDiGetDeviceInstallParams 来检索设备的设备安装参数，然后调用 SetupDiSetDeviceInstallParams 为具有 DI_NEEDREBOOT 标志的设备设置 SP_DEVINSTALL_PARAMS 结构的 **标志** 成员。 安装程序还会通知用户需要重新启动系统。

-   如果完成安装操作失败，但在下次枚举设备时应再次尝试完成安装操作，则类安装程序会将此情况的用户通知给用户。

    **注意**   从 Windows 8 开始，"完成-安装" 操作只运行一次。 Windows 不会再次自动运行它，特别是在下次枚举设备时不会自动运行，因为这不是在运行时执行的。

     

-   如果完成安装操作失败并且类安装程序确定完成安装操作无法成功，则类安装程序会将这种情况的用户通知给用户。

-   默认情况下，如果完成安装操作成功或完成安装操作失败，并且安装程序确定不应再次尝试执行安装操作，则类安装程序将为响应 DIF_FINISHINSTALL_ACTION 请求返回 ERROR_DI_DO_DEFAULT。 仅当完成安装操作失败，并且在下一次在管理员上下文中枚举设备时应再次尝试完成安装操作时，安装程序才返回 Win32 错误代码。

    **注意**   从 Windows 8 开始，"完成-安装" 操作只运行一次。 Windows 不会再次自动运行它，特别是在下次枚举设备时不会自动运行，因为这不是在运行时执行的。

     

下面的类安装程序代码示例演示实现完成安装操作的类安装程序代码的基本结构：

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

 

