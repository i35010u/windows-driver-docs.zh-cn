---
title: 自托管桌面驱动程序的测试分发指南
description: 自托管桌面驱动程序的测试分发指南
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 132bb46310042d5f4d39a9fcca07fb1e110e3572
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800329"
---
# <a name="test-distribution-guidance-to-self-host-desktop-drivers"></a>自托管桌面驱动程序的测试分发指南


硬件合作伙伴可以通过将驱动程序发布到 Windows 更新并使用测试分发，来测试操作系统升级方案。 在发布后，IHV/OEM 可通过配置预定义的注册表项值来配置他们的客户端系统，从而请求这些驱动程序。 除了接收为进行测试而分配的驱动程序，生产驱动程序仍将提供给相同的客户端计算机。 这将向由 Windows 更新提供的生产驱动程序列表添加预发布驱动程序。 此方法限制了向公众提供预发布驱动程序。

从 Windows 10 开始，客户端系统可能会在整个 Windows 升级过程中参与接收测试分配驱动程序。 硬件合作伙伴可使用此测试分发过程测试操作系统升级方案。

## <a name="span-idwhat_is_test_distribution__and_why_do_i_need_it_spanspan-idwhat_is_test_distribution__and_why_do_i_need_it_spanspan-idwhat_is_test_distribution__and_why_do_i_need_it_spanwhat-is-test-distribution-and-why-do-i-need-it"></a><span id="What_is_test_distribution__and_why_do_I_need_it_"></span><span id="what_is_test_distribution__and_why_do_i_need_it_"></span><span id="WHAT_IS_TEST_DISTRIBUTION__AND_WHY_DO_I_NEED_IT_"></span>测试分发是什么，我为什么需要它？


通过发布测试分发驱动程序并配置客户端系统以接收测试分配驱动程序，你可以使该系统接收在 Windows 更新上发布的所有预发布驱动程序和固件内容。 这允许合作伙伴使用 Windows 更新向他们的测试受众发布驱动程序，而不会影响其零售消费者受众。

## <a name="span-idpublishing_drivers_with_test_distributionspanspan-idpublishing_drivers_with_test_distributionspanspan-idpublishing_drivers_with_test_distributionspanpublishing-drivers-with-test-distribution"></a><span id="Publishing_drivers_with_test_distribution"></span><span id="publishing_drivers_with_test_distribution"></span><span id="PUBLISHING_DRIVERS_WITH_TEST_DISTRIBUTION"></span>使用测试分发发布驱动程序


可以发布适用于 Windows 7、Windows 8.x 和 Windows 10 系统的测试分发驱动程序。 若要发布测试分发，通常只需[创建发货标签](manage-driver-distribution-by-submission.md)，然后单击“设定目标”部分中的“测试注册表项”复选框。

![显示“测试注册表项”复选框的图像](images/test-registry-key-checkbox.png)

## <a name="span-idremoving_drivers_published_for_test_distributionspanspan-idremoving_drivers_published_for_test_distributionspanspan-idremoving_drivers_published_for_test_distributionspanremoving-drivers-published-for-test-distribution"></a><span id="Removing_drivers_published_for_test_distribution"></span><span id="removing_drivers_published_for_test_distribution"></span><span id="REMOVING_DRIVERS_PUBLISHED_FOR_TEST_DISTRIBUTION"></span>删除针对测试分发发布的驱动程序


### <a name="span-idhow_do_i_manually_remove_my_driver_published_for_test_distribution_spanspan-idhow_do_i_manually_remove_my_driver_published_for_test_distribution_spanspan-idhow_do_i_manually_remove_my_driver_published_for_test_distribution_spanhow-do-i-manually-remove-my-driver-published-for-test-distribution"></a><span id="How_do_I_manually_remove_my_driver_published_for_test_distribution_"></span><span id="how_do_i_manually_remove_my_driver_published_for_test_distribution_"></span><span id="HOW_DO_I_MANUALLY_REMOVE_MY_DRIVER_PUBLISHED_FOR_TEST_DISTRIBUTION_"></span>如何手动删除为测试分发发布的驱动程序？

针对测试分发发布驱动程序后，可以针对（正常）分发手动使其失效或重新发布。

### <a name="span-idhow_long_does_my_driver_published_for_test_distribution_last_spanspan-idhow_long_does_my_driver_published_for_test_distribution_last_spanspan-idhow_long_does_my_driver_published_for_test_distribution_last_spanhow-long-does-my-driver-published-for-test-distribution-last"></a><span id="How_long_does_my_driver_published_for_test_distribution_last_"></span><span id="how_long_does_my_driver_published_for_test_distribution_last_"></span><span id="HOW_LONG_DOES_MY_DRIVER_PUBLISHED_FOR_TEST_DISTRIBUTION_LAST_"></span>为测试分发发布的驱动程序的有效期是多长时间？

驱动程序不会自动从测试分发工作流中过期。 完成测试后，使用[通过 Windows 更新使驱动程序过期](expire-a-driver-from-windows-update.md)中所述的过程手动删除驱动程序。

## <a name="span-idclient_pc_configurationspanspan-idclient_pc_configurationspanspan-idclient_pc_configurationspanclient-pc-configuration"></a><span id="Client_PC_configuration"></span><span id="client_pc_configuration"></span><span id="CLIENT_PC_CONFIGURATION"></span>客户端电脑配置

### <a name="span-idhow_do_i_configure_my_machine_to_receive_test_distribution_drivers_spanspan-idhow_do_i_configure_my_machine_to_receive_test_distribution_drivers_spanspan-idhow_do_i_configure_my_machine_to_receive_test_distribution_drivers_spanhow-do-i-configure-my-machine-to-receive-test-distribution-drivers"></a><span id="How_do_I_configure_my_machine_to_receive_test_distribution_drivers_"></span><span id="how_do_i_configure_my_machine_to_receive_test_distribution_drivers_"></span><span id="HOW_DO_I_CONFIGURE_MY_MACHINE_TO_RECEIVE_TEST_DISTRIBUTION_DRIVERS_"></span>如何配置我的计算机以接收测试分发驱动程序？

可以执行以下步骤以将系统配置为接收测试分发更新：

1.  打开 Windows 注册表编辑器 (regedit.exe)
2.  转到 HKLM\\Software\\Microsoft\\
3.  创建子项 \\DriverFlighting\\Partner\\
4.  在 \\Partner 子项下，创建名为“TargetRing”  的字符串并键入“Drivers”  作为值
5.  确保你按如下所示内容进行了设置：

    ![显示 Windows 注册表编辑器中合作伙伴子项下创建的字符串的图像](images/registry-editor-drivers.png)

6.  退出 Windows 注册表编辑器。 你不需要在做出此更改后重新启动计算机。
7.  执行下列操作之一：
    -   运行 Windows Update 并检查更新。
    -   在设备管理器中，右键单击目标设备并“更新设备软件”  。
8.  验证是否按照预期提供了测试驱动程序

    -   如果遇到问题，请联系客户服务和支持人员。

        ![显示用于联系客户服务和支持人员的按钮的图像](images/dashboard-help-button.png)

### <a name="span-idhow_do_i_stop_my_pc_from_receiving_test_distribution_drivers_spanspan-idhow_do_i_stop_my_pc_from_receiving_test_distribution_drivers_spanspan-idhow_do_i_stop_my_pc_from_receiving_test_distribution_drivers_spanhow-do-i-stop-my-pc-from-receiving-test-distribution-drivers"></a><span id="How_do_I_stop_my_PC_from_receiving_test_distribution_drivers_"></span><span id="how_do_i_stop_my_pc_from_receiving_test_distribution_drivers_"></span><span id="HOW_DO_I_STOP_MY_PC_FROM_RECEIVING_TEST_DISTRIBUTION_DRIVERS_"></span>如何使我的电脑停止接收测试分发驱动程序？

若要停止接收测试分发驱动程序，请删除你在先前部分中创建的“TargetRing”  注册表数据值。 双击“Drivers”  数据值将其删除，然后单击“确定”  。 通过执行此操作，将不再向你的客户端系统提供预发布驱动程序。

**注意**  你的系统将继续从 Windows 更新接收所有生产驱动程序。

 

1.  打开 Windows 注册表编辑器 (regedit.exe)
2.  转到 HKLM\\Software\\Microsoft\\DriverFlighting\\Partner。 如果这些项不存在，则已完成操作，否则继续执行下一步。
3.  在 \\Partner 子项下，删除“TargetRing”  的数据值
4.  确保设置如下所示：

    ![显示 Windows 注册表编辑器中合作伙伴子项下已删除的字符串值的图像](images/registry-editor-no-drivers.png)

5.  退出 Windows 注册表编辑器。 你不需要在做出此更改后重新启动计算机。
6.  执行下列操作之一：
    -   运行 Windows 更新并检查更新
    -   在设备管理器中，右键单击目标设备并选择 **更新设备软件**。

 

 





