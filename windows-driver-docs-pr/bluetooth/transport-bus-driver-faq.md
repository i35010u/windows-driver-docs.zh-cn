---
title: 传输总线驱动程序常见问题解答
description: 以下是常见的问题、 方案和问题的驱动程序开发人员可能会遇到开发总线驱动程序以支持蓝牙功能时。
ms.assetid: 7189EB3B-E071-4145-8308-EFA6D4E89D4B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 172d5d753747d46a60c1b563542d588c1eb31021
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328183"
---
# <a name="transport-bus-driver-faq"></a>传输总线驱动程序常见问题解答


以下是常见的问题、 方案和问题的驱动程序开发人员可能会遇到开发总线驱动程序以支持蓝牙功能时。

## <a name="span-idmyserialbusdriverencounteredsomeerrorwhatdoesitmeanspanspan-idmyserialbusdriverencounteredsomeerrorwhatdoesitmeanspanmy-serial-bus-driver-encountered-some-error-what-does-it-mean"></a><span id="my_serial_bus_driver_encountered_some_error._what_does_it_mean_"></span><span id="MY_SERIAL_BUS_DRIVER_ENCOUNTERED_SOME_ERROR._WHAT_DOES_IT_MEAN_"></span>我的串行总线驱动程序时遇到一些错误。 它是什么意思？


代码 10 49:[设备管理器生成的错误代码的说明](http://support.microsoft.com/kb/310123)。

代码 51:当串行总线驱动程序依赖于控制器驱动程序 （如 ACPI 表中所定义） 时，系统将在加载串行总线驱动程序，但它将不开始直到所有其依赖的驱动程序已成功启动。 当控制器驱动程序不存在或未加载成功，代码 51 错误触发。

代码 52 = 未签名驱动程序。

这些主题中的更详细地介绍驱动程序签名：

-   [驱动程序签名](https://msdn.microsoft.com/library/windows/hardware/ff544865)
-   [Windows 驱动程序签名要求](https://msdn.microsoft.com/windows/hardware/gg487317)

## <a name="span-idwhyismyserialbusdrivernotgettinganyioctlsfromthebluetoothcorestackspanspan-idwhyismyserialbusdrivernotgettinganyioctlsfromthebluetoothcorestackspanspan-idwhyismyserialbusdrivernotgettinganyioctlsfromthebluetoothcorestackspanwhy-is-my-serial-bus-driver-not-getting-any-ioctls-from-the-bluetooth-core-stack"></a><span id="Why_is_my_serial_bus_driver_not_getting_any_IOCTLs_from_the_Bluetooth_core_stack_"></span><span id="why_is_my_serial_bus_driver_not_getting_any_ioctls_from_the_bluetooth_core_stack_"></span><span id="WHY_IS_MY_SERIAL_BUS_DRIVER_NOT_GETTING_ANY_IOCTLS_FROM_THE_BLUETOOTH_CORE_STACK_"></span>为什么我串行总线驱动程序未获得任何 Ioctl 从蓝牙核心堆栈？


串行总线驱动程序可能已启用空闲状态的功能，但未实现电源控制处理部分和及其子主题中讨论的机制。 在此情况下，在蓝牙 HID 设备 （鼠标或键盘） 将无法唤醒堆栈 （从到 D0 D2)。 建议将关闭此空闲状态的功能，直到已实现基本的蓝牙功能和电源控制处理机制。

## <a name="span-idaretherebluetoothwindowslogotestsspanspan-idaretherebluetoothwindowslogotestsspanspan-idaretherebluetoothwindowslogotestsspanare-there-bluetooth-windows-logo-tests"></a><span id="Are_there_Bluetooth_Windows_Logo_Tests_"></span><span id="are_there_bluetooth_windows_logo_tests_"></span><span id="ARE_THERE_BLUETOOTH_WINDOWS_LOGO_TESTS_"></span>是否有蓝牙 Windows 徽标测试？


Windows HCK （硬件认证工具包） 包含一组特定于蓝牙的测试，必须在接收证书。 蓝牙驱动程序开发人员应在开发以确保其驱动程序将其要接收证书，使正确支持传递过程中运行这些测试。

## <a name="span-idshoulduartsettingsbepreservedandrestoredamongthedifferentpowerstatetransitionsspanspan-idshoulduartsettingsbepreservedandrestoredamongthedifferentpowerstatetransitionsspanspan-idshoulduartsettingsbepreservedandrestoredamongthedifferentpowerstatetransitionsspanshould-uart-settings-be-preserved-and-restored-among-the-different-power-state-transitions"></a><span id="Should_UART_settings_be_preserved_and_restored_among_the_different_power_state_transitions_"></span><span id="should_uart_settings_be_preserved_and_restored_among_the_different_power_state_transitions_"></span><span id="SHOULD_UART_SETTINGS_BE_PRESERVED_AND_RESTORED_AMONG_THE_DIFFERENT_POWER_STATE_TRANSITIONS_"></span>应 UART 设置进行保留和还原在不同的电源状态转换？


因为蓝牙传输驱动程序已意识到，并且可以控制远程 UART 控制器的设置 （包括其设置后上提供支持），蓝牙传输驱动程序应重置两个远程和本地 UART 控制器在输入中的状态之前哪些电源可能会丢失。 因此，还原电源后，远程 UART （蓝牙端） 和本地 UART （宿主端） 控制器上的设置可能会保持同步。UART 驱动程序已对本地 UART 控制器的控制，并将负责之前还原为其设置。 蓝牙传输驱动程序还可以查询有关其强化设置 UART 驱动程序 （因为 UART 驱动程序将设置其最初使用 ACPI 表）、 缓存和输入一些 Dx 状态时将其设置。

## <a name="span-idwhathappensifthebusdriverreceivesawakenotificationwhilethestackisintheprocessofenteringd2spanspan-idwhathappensifthebusdriverreceivesawakenotificationwhilethestackisintheprocessofenteringd2spanspan-idwhathappensifthebusdriverreceivesawakenotificationwhilethestackisintheprocessofenteringd2spanwhat-happens-if-the-bus-driver-receives-a-wake-notification-while-the-stack-is-in-the-process-of-entering-d2"></a><span id="What_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_D2_"></span><span id="what_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_d2_"></span><span id="WHAT_HAPPENS_IF_THE_BUS_DRIVER_RECEIVES_A_WAKE_NOTIFICATION_WHILE_THE_STACK_IS_IN_THE_PROCESS_OF_ENTERING_D2_"></span>如果总线驱动程序收到唤醒通知过程中进入 D2 堆栈时，会发生什么情况？


在此情况下，总线驱动程序应完成 D2 转换，并继续唤醒机制。 串行总线驱动程序应执行此同步 （例如可以唤醒请求进行排队并仅在 D2 转换完成后启动唤醒过程）。

## <a name="span-idhowshouldabusdriveridentifyitsacpiresourceofmultipleoccurrencessuchasmultiplegpiosspanspan-idhowshouldabusdriveridentifyitsacpiresourceofmultipleoccurrencessuchasmultiplegpiosspanspan-idhowshouldabusdriveridentifyitsacpiresourceofmultipleoccurrencessuchasmultiplegpiosspanhow-should-a-bus-driver-identify-its-acpi-resource-of-multiple-occurrences-such-as-multiple-gpios"></a><span id="How_should_a_bus_driver_identify_its_ACPI_resource_of_multiple_occurrences__such_as_multiple_GPIOs_"></span><span id="how_should_a_bus_driver_identify_its_acpi_resource_of_multiple_occurrences__such_as_multiple_gpios_"></span><span id="HOW_SHOULD_A_BUS_DRIVER_IDENTIFY_ITS_ACPI_RESOURCE_OF_MULTIPLE_OCCURRENCES__SUCH_AS_MULTIPLE_GPIOS_"></span>总线驱动程序应如何标识多个匹配项，如多个 GPIOs 其 ACPI 资源？


没有方法来标记资源，GPIO 或其他。 这就是原因资源顺序非常重要。 设备驱动程序应建立一个约定 (例如要显示在列表中的第一个 GPIO 资源为 BT\_出现唤醒和第二个是宿主\_唤醒)。

 

 





