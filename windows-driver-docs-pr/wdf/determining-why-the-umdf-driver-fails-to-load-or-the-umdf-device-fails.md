---
title: 确定 UMDF 驱动程序加载失败的原因或设备无法启动
description: 本主题介绍可以使用 UMDF 驱动程序将无法加载或关联的设备无法启动时的故障排除步骤。
ms.assetid: 366c0ab4-8d06-4dac-a301-f433cf7978bd
keywords:
- 调试方案 WDK UMDF，UMDF 驱动程序加载失败
- 调试方案 WDK UMDF，UMDF 设备无法启动
- UMDF WDK，调试方案，UMDF 驱动程序加载失败
- UMDF WDK，调试方案，UMDF 设备无法启动
- UMDF WDK，驱动程序未加载方案
- UMDF WDK，设备无法启动方案
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b892e4c89d17b512ce41ad18040d30bd224b3da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545029"
---
# <a name="determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails-to-start"></a>确定 UMDF 驱动程序将无法加载或 UMDF 设备启动失败的原因


本主题介绍可以使用 UMDF 驱动程序将无法加载或关联的设备无法启动时的故障排除步骤。

使用这两种 UMDF 版本 1 和 2 的驱动程序，可以使用以下技术。

1.  通过确保以下文件正确的检查安装程序：
    -   驱动程序的 INF 文件。

        使用[ChkINF](https://msdn.microsoft.com/library/windows/hardware/ff543461)工具验证驱动程序的 INF 文件。

    -   %windir%\\inf\\setupapi.dev.log (setupapi.log Windows XP 上)、 %windir%\\setupact.log、 和 %windir%\\temp\\wudf\_update.log 文件。

2.  如果未找到任何安装问题，启用**HostProcessDbgBreakOnStart**通过使用注册表项[WDF 验证程序控件应用程序](https://msdn.microsoft.com/library/windows/hardware/ff556129)(WdfVerifier.exe)。 通过启用**HostProcessDbgBreakOnStart**、 将调试程序不久后 WUDFHost.exe 开始到以设备 (WUDFHost.exe) 中断的驱动程序主机进程，但之前您的驱动程序 DLL 加载。

    应启用**HostProcessDbgBreakOnStart**使用用户模式下调试程序和不内核模式调试程序。 不，内核模式调试程序，默认情况下，不会接收用户模式模块加载和卸载通知。 因此，您将不能设置延迟的断点。

3.  如果看不到启动的主机，请执行以下步骤来正确配置设备：
    1.  请确保您通过在 INF 安装的所有驱动程序存在，并且复制到操作系统。
    2.  如果该发送程序 (也称为 WUDFRd.sys) 不是设备上的服务，请确保该驱动程序，然后将该服务，有一个服务的条目 (例如，为 sc qc foo)，并设置为自动启动。

4.  确保您的驱动程序的符号在符号路径 (即，.sympath)。

5.  一次验证以下各项的一个。 在以下步骤中，假设您的驱动程序为：
    1.  验证您的驱动程序**DllMain**例程调用 （例如，bu Foo ！DllMain)。
    2.  如果 does 加载驱动程序 DLL，为执行后续步骤，还可以使用**HostProcessDbgBreakOnDriverLoad**注册表项。 无**HostProcessDbgBreakOnDriverLoad**集导致 WUDFHost.exe 若要在您的驱动程序加载 DLL 后进入调试器。 **HostProcessDbgBreakOnDriverLoad**可以也在内核模式调试程序因为此时正在加载的驱动程序和设备在启动过程中您可以设置断点在驱动程序代码中。
    3.  此步骤适用于 UMDF 版本 1 驱动程序。 验证您的驱动程序**DllGetClassObject**调用例程。 验证您的驱动程序的类标识符 (ID) 正确。 确认**DllGetClassObject**成功运行，并返回驱动程序对象 (例如，bu Foo ！DllGetClassObject)。

    4.  对于 UMDF 版本 1，请验证您的驱动程序[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)调用方法。 验证该方法将创建一个设备，并返回成功 （例如，bu Foo ！CMyDriver::OnDeviceAdd)。

        对于 UMDF 版本 2，请验证您的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)调用函数。 验证该函数将创建一个设备，并返回成功 （例如，bu Foo ！MyDriverDeviceAdd)。

    5.  对于 UMDF 版本 1，请验证您的驱动程序[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)或[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)调用方法。 验证该方法返回成功 （例如，bu Foo ！CMyDevice::OnPrepareHardware 或 Foo ！CMyDevice::OnD0Entry)。

        对于 UMDF 版本 2，请验证您的驱动程序[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)或[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)调用函数。 验证该函数返回成功 （例如，bu Foo ！MyDevicePrepareHardware 或 Foo ！MyDeviceD0Entry)。

    6.  如果每个成功运行了上一操作，而且后面的运算不会运行，则应检查以下各项：
        1.  验证每个驱动程序的上方和下方您在用户模式堆栈中的驱动程序也成功地执行这些操作。
        2.  验证是否已成功完成下您的驱动程序的内核堆栈[ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)并[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749) Irp。

 

 





