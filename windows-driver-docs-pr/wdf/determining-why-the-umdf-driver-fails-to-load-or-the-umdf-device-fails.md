---
title: 确定无法加载 UMDF 驱动程序或设备启动失败的原因
description: 本主题介绍在 UMDF 驱动程序无法加载或相关设备无法启动时可以使用的故障排除步骤。
ms.assetid: 366c0ab4-8d06-4dac-a301-f433cf7978bd
keywords:
- 调试方案 WDK UMDF，UMDF 驱动程序加载失败
- 调试方案 WDK UMDF，UMDF 设备无法启动
- UMDF WDK，调试方案，UMDF 驱动程序加载失败
- UMDF WDK，调试方案，UMDF 设备无法启动
- UMDF WDK，驱动程序未加载方案
- UMDF WDK，设备未启动方案
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae98201f8cb6ec71b1f6de61b3443451f5ca547
ms.sourcegitcommit: b3bcd94c24b19b4c76c3b49672e237af03b3a7f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82173519"
---
# <a name="determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails-to-start"></a>确定 UMDF 驱动程序无法加载或 UMDF 设备无法启动的原因


本主题介绍在 UMDF 驱动程序无法加载或相关设备无法启动时可以使用的故障排除步骤。

可以在 UMDF 版本1和2驱动程序中使用以下技术。

1.  通过确保以下文件正确来检查设置：
    -   驱动程序的 INF 文件。

        使用[InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)工具验证驱动程序的 INF 文件。

    -   % windir%\\inf\\\\setupapi.log （Windows XP 上的 setupapi.log）、% windir% setupact.log 和% windir%\\temp\\wudf\_更新日志文件。

2.  如果未找到任何安装问题，请通过使用[WDF 验证器控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)（您尚未 wdfverifier）来启用**HostProcessDbgBreakOnStart**注册表项。 通过启用**HostProcessDbgBreakOnStart**，你将在 WUDFHost 启动之后但在加载驱动程序 DLL 之前，将设备的驱动程序宿主进程（WUDFHost）立即进入调试器。

    应使用用户模式调试器而不是内核模式调试器来启用**HostProcessDbgBreakOnStart** 。 默认情况下，内核模式调试器不接收用户模式模块加载和卸载通知。 因此，您将无法设置延迟断点。

3.  如果看不到主机启动，请执行以下步骤以正确配置设备：
    1.  确保通过 INF 安装的所有驱动程序都存在并复制到操作系统。
    2.  如果反射器（也称为 WUDFRd）不是设备上的服务，请确保驱动程序（随后将作为服务）具有服务项（例如，"sc qc foo"），并将设置为自动启动。

4.  确保驱动程序的符号位于符号路径中（即 sympath）。

5.  一次验证一个项目。 在以下步骤中，假定你的驱动程序为 foo .dll：
    1.  验证是否调用了驱动程序的**DllMain**例程（例如，bu Foo！DllMain）。
    2.  如果驱动程序 DLL 已加载，则在后续步骤中，还可以使用**HostProcessDbgBreakOnDriverLoad**注册表项。 设置**HostProcessDbgBreakOnDriverLoad**后，WUDFHost 会在加载驱动程序 DLL 后中断到调试器。 **HostProcessDbgBreakOnDriverLoad**也可用于内核模式调试器，因为在驱动程序加载和设备启动过程中，你可以在驱动程序代码中设置断点。
    3.  此步骤仅适用于 UMDF 版本1驱动程序。 验证是否调用了驱动程序的**DllGetClassObject**例程。 验证驱动程序的类标识符（ID）是否正确。 验证**DllGetClassObject**是否成功运行并返回驱动程序对象（例如，bu Foo！DllGetClassObject）。

    4.  对于 UMDF 版本1，请验证是否调用了驱动程序的[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法。 验证方法是否创建了设备并成功返回（例如，bu Foo！CMyDriver::OnDeviceAdd).

        对于 UMDF 版本2，请验证是否调用了驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)函数。 验证该函数是否创建了一个设备并成功返回（例如，bu Foo！MyDriverDeviceAdd).

    5.  对于 UMDF 版本1，请验证是否调用了驱动程序的[**IPnpCallbackHardware：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)或[**IPnpCallback：： OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)方法。 验证该方法是否成功返回（例如，bu Foo！CMyDevice：： OnPrepareHardware 或 Foo！CMyDevice::OnD0Entry).

        对于 UMDF 版本2，请验证是否调用了驱动程序的[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)或[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)函数。 验证函数是否成功返回（例如，bu Foo！MyDevicePrepareHardware 或 Foo！MyDeviceD0Entry).

    6.  如果前面的每个操作都已成功运行，但随后执行的操作未运行，则应检查以下各项：
        1.  验证用户模式堆栈中的驱动程序上方和下方的每个驱动程序是否也成功执行这些操作。
        2.  验证驱动程序下面的内核堆栈是否已成功完成[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)和[**irp\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)irp。

 

 





