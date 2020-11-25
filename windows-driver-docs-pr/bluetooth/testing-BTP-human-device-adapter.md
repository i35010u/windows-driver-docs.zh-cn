---
title: Microsoft 蓝牙测试平台-人工设备适配器
description: )  (设备适配器的蓝牙测试平台 (HDA) 设置和配对
ms.date: 11/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: f6b9a16c205e2e0734569ca7d7f175a8c838457d
ms.sourcegitcommit: e184d264c55f0e7e224837ce39ee976ccb4122c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/24/2020
ms.locfileid: "95861731"
---
# <a name="bluetooth-test-platform---human-device-adapter"></a>蓝牙测试平台-人工设备适配器

个人设备适配器 (HDA) 是手动与 [蓝牙测试平台 (BTP) ](testing-BTP-Overview.md)交互的方式，允许使用 BTP 的设备，这些设备尚未自动执行。 例如，HDA 可以与购买的耳机交互，否则无法明确地连接到 BTP。 HDA 允许在 Windows 设备和原型制作硬件之间进行手动用户测试，而无需使用外部硬件，如 Traduci。 因此，设置所需的全部都是支持蓝牙和你自己的测试设备的 PC。  

## <a name="hda-set-up"></a>HDA 设置

安装 [BTP 软件安装程序](testing-BTP-setup.md#software-setup) 中所述的软件以支持 HDA。

## <a name="hda-configuration-file"></a>HDA 配置文件

创建一个配置文件，如下所示，在测试设备后命名为： *mytestdevice.txt*。 请注意，文件和扩展并不重要。

```console
name=myTestDevice
baseband=BR
br_address=B4:F1:DA:96:C0:A4
```

## <a name="hda-pairing-tests"></a>HDA 配对测试

导航到提取 BTP 软件包的文件夹（通常为） `C:\BTP` 。 下面引用的脚本将位于包目录的子文件夹中。 针对所需的命令环境运行相应的脚本：

| 命令环境 | Script |
| --- | --- |
| 提升的命令提示符 | `RunPairingTests.bat HDA,conf_file=<configuration file name>` |
| 提升的 PowerShell 控制台 | `RunPairingTests.ps1 HDA,conf_file=<configuration file name>` |

可以添加可选的参数 `-VerboseLogs` ，以提供 BTP 的内部操作的更详细输出，以帮助进行调试。

## <a name="hda-manual-pairing"></a>HDA 手动配对

1. 此脚本将按如下方式进行响应，并询问设备是否已配对。 如果输入了 "y"，则会删除配对;如果输入了 "n"，则进程将继续执行，而不执行任何操作。

    ```console
    Verify: SUCCEEDED(WEX::TestExecution::RuntimeParameters::TryGetValue(deviceParameterName.c_str(), deviceParametersStr)): Getting required runtime parameter 'central'
    [BluetoothTests::PairingTestsImpl::PairingTestsImpl]: Using central device named: MyCentralDevice
    [BluetoothTests::PairingTestsImpl::PairingTestsImpl]: Using peripheral device named: MyTestDevice
    [BluetoothTestHelpers::Pairing::Unpair]: Unpairing device with address B4F1DA96C0A4 from the device with address D83BBFAC35607
    [BluetoothTestHelpers::Pairing::Unpair]: Unpaired successfully
    [BluetoothTestHelpers::Pairing::WaitForDisconnection]: Waiting for disconnection of device with address B4F1DA96C0A4
    [BluetoothTestHelpers::Pairing::WaitForDisconnection]: Asserted: connectionModule.WaitForDisconnection(otherDeviceAddress, c_disconnectionAfterUnpairingTimeout)
    [BluetoothTestHelpers::Pairing::WaitForDisconnection]: Disconnected successfully
    Is MyTestDevice paired to the device with address D83BBFAC35607?
    Enter (y/n): y
    ```

    下面是删除配对的 HDA 的示例。 它还将在名为 "MyTestDevice" ) 的设备 (上删除任何配对信息。 删除任何配对信息后，按任意键继续。

    ```console
    [BluetoothTestHelpers::Pairing::Unpair]: Unpairing device with address D83BBFAC35607 Public from the device with address D83BBFAC35607 Public
    If possible, delete the pairing on MyTestDevice
    Press any key to continue
    ```

2. 然后，该脚本通过运行检查来开始配对过程，然后提示用户输入其设备 (名为 "MyTestDevice" ) 为 "*带区* 配对模式"。 完成此操作后，按任意键继续。

    ```console
    StartGroup: BluetoothTests::TaefPairingTests::OutgoingJustWorksPairingTest
    [BluetoothTests::PairingTestsImpl::OutgoingJustWorksPairingTest]: Will attempt an outgoing pairing to the peripheral device and validate that a JustWorks ceremony was used
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: (originDeviceAssociationModule) != nullptr
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: originDeviceAssociationModule->CanInitiatePairing()
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: originDeviceAssociationModule->CanCheckPairingStatus()
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: !(originDeviceAssociationModule->IsPairedTo(destinationDeviceAddress))
    If not already, put MyTestDevice in BR pairing mode
    Press any key to continue . . .
    ```

3. 然后，该脚本将启动配对。 如果配对成功，输出将如下所示。 响应设备或测试 PC 上的任何通知，以确认并完成配对。 然后，该测试会提示设备进入配对模式。 完成此操作后，按任意键继续。

    ```console
    [BluetoothTestHelpers::Pairing::Pair]: Initiating pairing request from device with address D83BBFAC35607 to device with address B4F1DA96C0A4
    [BluetoothTestHelpers::Pairing::DefaultPairingCeremonyHandler::OnJustWorks]: JustWorks ceremony used
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: originDeviceAssociationModule->IsPairedTo(destinationDeviceAddress)
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: ceremonyHandler.GetLastCeremonyUsed().has_value()
    [BluetoothTestHelpers::Pairing::Pair]: Asserted: ceremonyHandler.GetLastCeremonyUsed().value() == expectedCeremony
    [BluetoothTestHelpers::Pairing::Pair]: Paired successfully
    If the device is in pairing mode, exit pairing mode if possible.
    Press any key to continue . . .
    ```

4. 配对完成后，脚本将继续到测试套件中可用的测试上。 在[当前支持的 BTP 测试](testing-BTP-Tests.md)中，可以找到有关可用测试以及如何运行这些测试的文档

## <a name="hda-log-capture"></a>HDA 日志捕获

如果遇到问题，则可以按照 [GitHub 上的 Busiotools For Windows](https://github.com/Microsoft/busiotools/tree/master/bluetooth/tracing)存储库上的说明捕获蓝牙日志的蓝牙日志进行日志捕获，或者在 `-VerboseLogs` 启动测试时使用脚本选项。

## <a name="see-also"></a>另请参阅

[蓝牙测试平台主页](testing-BTP-Overview.md)

[蓝牙测试平台软件设置](testing-BTP-setup.md#software-setup)

[蓝牙测试平台可用测试](testing-btp-tests.md)

[用于日志捕获的 GitHub 上的 Windows 存储库 Busiotools](https://github.com/Microsoft/busiotools/tree/master/bluetooth/tracing)
