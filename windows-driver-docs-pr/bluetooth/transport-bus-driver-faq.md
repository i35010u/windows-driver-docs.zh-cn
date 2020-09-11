---
title: 传输总线驱动程序常见问题解答
description: 下面是开发总线驱动程序时，驱动程序开发人员可能遇到的常见问题、方案和问题，以支持蓝牙功能。
ms.assetid: 7189EB3B-E071-4145-8308-EFA6D4E89D4B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba55576532344229154a99e0ec7ec5cfdf2a663
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010589"
---
# <a name="transport-bus-driver-faq"></a>传输总线驱动程序常见问题解答


下面是开发总线驱动程序时，驱动程序开发人员可能遇到的常见问题、方案和问题，以支持蓝牙功能。

## <a name="span-idmy_serial_bus_driver_encountered_some_error_what_does_it_mean_spanspan-idmy_serial_bus_driver_encountered_some_error_what_does_it_mean_spanmy-serial-bus-driver-encountered-some-error-what-does-it-mean"></a><span id="my_serial_bus_driver_encountered_some_error._what_does_it_mean_"></span><span id="MY_SERIAL_BUS_DRIVER_ENCOUNTERED_SOME_ERROR._WHAT_DOES_IT_MEAN_"></span>我的串行总线驱动程序遇到了一些错误。 它意味着什么？


代码10-49：对 [设备管理器生成的错误代码的说明](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows)。

代码51：当串行总线驱动程序具有从属控制器驱动程序 (如 ACPI 表) 中定义时，系统将加载串行总线驱动程序，但在其所有从属驱动程序均已成功启动之前，该驱动程序不会启动。 如果控制器驱动程序不存在或未成功加载，则会触发代码51错误。

代码 52 = 未签名的驱动程序。

以下主题更详细地介绍了驱动程序签名：

-   [驱动程序签名](../install/driver-signing.md)
-   [Windows 驱动程序签名要求](/previous-versions/windows/hardware/design/dn653563(v=vs.85))

## <a name="span-idwhy_is_my_serial_bus_driver_not_getting_any_ioctls_from_the_bluetooth_core_stack_spanspan-idwhy_is_my_serial_bus_driver_not_getting_any_ioctls_from_the_bluetooth_core_stack_spanspan-idwhy_is_my_serial_bus_driver_not_getting_any_ioctls_from_the_bluetooth_core_stack_spanwhy-is-my-serial-bus-driver-not-getting-any-ioctls-from-the-bluetooth-core-stack"></a><span id="Why_is_my_serial_bus_driver_not_getting_any_IOCTLs_from_the_Bluetooth_core_stack_"></span><span id="why_is_my_serial_bus_driver_not_getting_any_ioctls_from_the_bluetooth_core_stack_"></span><span id="WHY_IS_MY_SERIAL_BUS_DRIVER_NOT_GETTING_ANY_IOCTLS_FROM_THE_BLUETOOTH_CORE_STACK_"></span>为什么我的串行总线驱动程序无法从蓝牙核心堆栈获取任何 IOCTLs？


串行总线驱动程序可能已启用空闲功能，但未实现部分及其子主题中讨论的电源控制处理机制。 在这种情况下， (鼠标或键盘) 的蓝牙 HID 设备将无法将堆栈从 D2 (唤醒到 D0) 。 建议关闭此空闲功能，直到已实现基本蓝牙功能和电源控制处理机制。

## <a name="span-idare_there_bluetooth_windows_logo_tests_spanspan-idare_there_bluetooth_windows_logo_tests_spanspan-idare_there_bluetooth_windows_logo_tests_spanare-there-bluetooth-windows-logo-tests"></a><span id="Are_there_Bluetooth_Windows_Logo_Tests_"></span><span id="are_there_bluetooth_windows_logo_tests_"></span><span id="ARE_THERE_BLUETOOTH_WINDOWS_LOGO_TESTS_"></span>是否存在蓝牙 Windows 徽标测试？


Windows HCK (硬件认证包) 包含一组特定于蓝牙的测试，必须传递这些测试才能接收证书。 蓝牙驱动程序开发人员应在开发过程中运行这些测试，以确保其驱动程序可以通过进行认证并获得正确的支持。

## <a name="span-idshould_uart_settings_be_preserved_and_restored_among_the_different_power_state_transitions_spanspan-idshould_uart_settings_be_preserved_and_restored_among_the_different_power_state_transitions_spanspan-idshould_uart_settings_be_preserved_and_restored_among_the_different_power_state_transitions_spanshould-uart-settings-be-preserved-and-restored-among-the-different-power-state-transitions"></a><span id="Should_UART_settings_be_preserved_and_restored_among_the_different_power_state_transitions_"></span><span id="should_uart_settings_be_preserved_and_restored_among_the_different_power_state_transitions_"></span><span id="SHOULD_UART_SETTINGS_BE_PRESERVED_AND_RESTORED_AMONG_THE_DIFFERENT_POWER_STATE_TRANSITIONS_"></span>是否应在不同的电源状态转换中保留 UART 设置并进行还原？


由于蓝牙传输驱动程序可以识别并控制远程 UART 控制器的设置 (在开机) 后包含其设置，因此，蓝牙传输驱动程序应重置远程和本地 UART 控制器，然后再进入可能会丢失电源的状态。 因此，当电源恢复时，远程 UART 上的设置 (蓝牙端) 并且本地 UART (主机端) 控制器可以同步。UART 驱动程序只能控制本地 UART 控制器，并将负责在关机之前还原到其设置。 蓝牙传输驱动程序还可以在 UART 驱动程序上查询其电源设置 (因为 UART 驱动程序最初使用 ACPI 表将其设置) 、缓存并在进入 Dx 状态时进行设置。

## <a name="span-idwhat_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_d2_spanspan-idwhat_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_d2_spanspan-idwhat_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_d2_spanwhat-happens-if-the-bus-driver-receives-a-wake-notification-while-the-stack-is-in-the-process-of-entering-d2"></a><span id="What_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_D2_"></span><span id="what_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_d2_"></span><span id="WHAT_HAPPENS_IF_THE_BUS_DRIVER_RECEIVES_A_WAKE_NOTIFICATION_WHILE_THE_STACK_IS_IN_THE_PROCESS_OF_ENTERING_D2_"></span>如果在堆栈正在进入 D2 的过程中，总线驱动程序收到唤醒通知，会发生什么情况？


在这种情况下，总线驱动程序应完成 D2 转换，然后继续进入唤醒机制。 串行总线驱动程序应执行此同步 (例如，它可以将唤醒请求排队并仅在 D2 转换完成后启动唤醒过程) 。

## <a name="span-idhow_should_a_bus_driver_identify_its_acpi_resource_of_multiple_occurrences__such_as_multiple_gpios_spanspan-idhow_should_a_bus_driver_identify_its_acpi_resource_of_multiple_occurrences__such_as_multiple_gpios_spanspan-idhow_should_a_bus_driver_identify_its_acpi_resource_of_multiple_occurrences__such_as_multiple_gpios_spanhow-should-a-bus-driver-identify-its-acpi-resource-of-multiple-occurrences-such-as-multiple-gpios"></a><span id="How_should_a_bus_driver_identify_its_ACPI_resource_of_multiple_occurrences__such_as_multiple_GPIOs_"></span><span id="how_should_a_bus_driver_identify_its_acpi_resource_of_multiple_occurrences__such_as_multiple_gpios_"></span><span id="HOW_SHOULD_A_BUS_DRIVER_IDENTIFY_ITS_ACPI_RESOURCE_OF_MULTIPLE_OCCURRENCES__SUCH_AS_MULTIPLE_GPIOS_"></span>总线驱动程序应该如何识别其多个匹配项（例如多个 GPIOs）的 ACPI 资源？


无法标记资源、GPIO 或其他方法。 这就是资源顺序非常重要的原因。 设备驱动程序应建立约定 (例如，要在列表中显示的第一个 GPIO 资源适用于 BT \_ 唤醒，另一个要显示的是用于主机 \_ 唤醒) 。

 

