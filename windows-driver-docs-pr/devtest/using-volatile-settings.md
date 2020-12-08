---
title: 使用易失性设置
description: 使用易失性设置
keywords:
- 驱动程序验证程序 WDK，可变设置
- 可变设置 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bb877b8d8aeda0ef0d0aa4148c856715e6ed848
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787619"
---
# <a name="using-volatile-settings"></a>使用易失性设置


## <span id="ddk_using_volatile_settings_tools"></span><span id="DDK_USING_VOLATILE_SETTINGS_TOOLS"></span>


大多数对驱动程序验证程序状态的更改 (激活、停用、更改选项或更改正在) 验证的驱动程序列表，只在重新启动计算机 ( "重新启动" ) 时才会生效。

但是，可以在不重新启动的情况下激活和停用某些选项。 这些 *设置称为可变设置。* 对这些设置的更改将立即生效，最后一次启动时，或在再次更改之前进行。

本部分介绍了易失性设置，以及如何在不同版本的 Windows 中包含的驱动程序验证程序版本中使用这些设置。

### <a name="span-idchanging_options_without_rebootingspanspan-idchanging_options_without_rebootingspanchanging-options-without-rebooting"></a><span id="changing_options_without_rebooting"></span><span id="CHANGING_OPTIONS_WITHOUT_REBOOTING"></span>更改选项而不重新启动

你可以激活和停用所有的驱动程序验证程序选项，不需要重新启动计算机，但不包括 [DDI 相容性检查](ddi-compliance-checking.md)、 [Power Framework 延迟模糊](concurrency-stress-test.md)、 [Storport 验证](dv-storport-verification.md)、 [SCSI 验证](scsi-verification.md) 和 [磁盘完整性检查](disk-integrity-checking.md)。

**注意**  在 Windows Vista 之前的 Windows 版本中，你可以仅激活和停用下列驱动程序验证程序选项，而无需重新启动计算机。 但是，若要执行此操作，驱动程序验证程序必须已在运行，也就是说，必须至少用一个选项启动驱动程序验证程序，然后重新启动计算机。 运行后，可以激活和停用这些设置，而无需重新启动。
-   [特殊池](special-pool.md)

-   [强制 IRQL 检查](force-irql-checking.md)

-   [资源不足模拟](low-resources-simulation.md)

 

### <a name="span-idchanging_drivers_without_rebootingspanspan-idchanging_drivers_without_rebootingspanchanging-drivers-without-rebooting"></a><span id="changing_drivers_without_rebooting"></span><span id="CHANGING_DRIVERS_WITHOUT_REBOOTING"></span>更改驱动程序而不重新启动

从 Windows Vista 开始，你可以添加和删除驱动程序 (即，启动和停止对驱动程序的验证) 无需重新启动计算机，即使驱动程序验证器尚未运行也是如此。

你还可以在不重新启动的情况下开始验证已加载的驱动程序，但无法在不重新启动的情况下停止对已加载的驱动程序的验证。 加载并验证驱动程序后，Driver Verifier 会监视它，直到下一次重新启动，但你可以在不重新启动的情况下关闭驱动程序的驱动程序验证器可选检查，从而最大限度地减少驱动程序验证程序开销。

在 Windows XP 和 Windows Server 2003 中，你可以在不重新启动的情况下添加和删除驱动程序，但前提是当前未加载驱动程序。

你可以通过使用 [**验证程序命令行**](verifier-command-line.md)或驱动程序验证器管理器来更改可变设置。 驱动程序验证器管理器有两个版本-一个适用于 [windows 2000](driver-verifier-manager--windows-2000-.md) ，一个用于 [windows XP 和更高](driver-verifier-manager--windows-xp-and-later-.md)版本。

### <a name="span-idvolatile_and_registry_settingsspanspan-idvolatile_and_registry_settingsspanvolatile-and-registry-settings"></a><span id="volatile_and_registry_settings"></span><span id="VOLATILE_AND_REGISTRY_SETTINGS"></span>可变和注册表设置

如果能够在不重新启动的情况下添加和更改驱动程序和设置选项，这是一项很重要的便利，并使你能够在某些不可能出现的测试方案中运行驱动程序验证程序。

不过，由于将驱动程序验证程序设置添加到注册表的传统模型有一些优点，因此需要决定是否要使用可变方法，或在注册表中设置这两种方法。

-   可变或 "运行时" 设置将立即生效，但当你关闭或重新启动 Windows 时，这些设置会丢失。

-   注册表设置需要重新启动，但它们保留在注册表中，直到你更改它们并再次重新启动。

应将在加载驱动程序时使用的或需要测量的设置添加到注册表中。 其他设置可以在需要时启用。

同时使用注册表设置和易失性设置时，请记住使用可变设置，而不是注册表设置;它们不会添加。

### <a name="span-idconfiguring_volatile_settings_by_using_the_verifier_command_linespanspan-idconfiguring_volatile_settings_by_using_the_verifier_command_linespanconfiguring-volatile-settings-by-using-the-verifier-command-line"></a><span id="configuring_volatile_settings_by_using_the_verifier_command_line"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_THE_VERIFIER_COMMAND_LINE"></span>使用验证器命令行配置可变设置

若要添加或删除可变选项，请使用 **/volatile/flags** 参数。

 (Windows XP 和更高版本中) 若要在可变列表中添加或删除驱动程序，请使用 **/volatile/adddriver** 或 **/volatile/removedriver** 参数。 有关详细信息，请参阅 [**驱动程序验证程序命令语法**](verifier-command-line.md) 。

-   若要在不重新启动的情况下启动或停止对驱动程序的验证：

    ```
    verifier /volatile /adddriver DriverName.sys
    verifier /volatile /removedriver DriverName.sys
    ```

    您可以使用此命令语法来添加 (启动所有驱动程序的验证) ，甚至是当前加载的驱动程序。 用于删除 (停止当前加载的驱动程序) 验证的命令将会失败。 与往常一样，加载驱动程序后，将立即验证未加载的驱动程序。

-   激活或停用选项而不重新启动：

    ```
    verifier /volatile /flags Options
    ```

    除了 [SCSI 验证](scsi-verification.md) 和 [磁盘完整性检查](disk-integrity-checking.md)以外，还可以将此命令语法用于任何驱动程序验证程序选项。 例如，

    ```
    verifier /volatile /flags 0x20
    ```

    此命令激活 [死锁检测](deadlock-detection.md) 选项，无需重新启动。

-   若要关闭所有驱动程序验证程序选项：

    你无法在不重新启动的情况下停止对当前加载的驱动程序的验证。 但是，可以使用以下命令语法停用所有的驱动程序验证程序选项而无需重新启动，从而最大限度地降低开销，直到下一次重新启动。

    ```
    verifier /volatile /flags 0
    ```

    驱动程序验证程序将继续使用 [自动检查](automatic-checks.md) 功能中的选项来监视驱动程序，该功能不能关闭，但开销减少到了典型验证的开销的大约10%。

### <a name="span-idconfiguring_volatile_settings_by_using_driver_verifier_manager__windows2kspanspan-idconfiguring_volatile_settings_by_using_driver_verifier_manager__windows2kspanspan-idconfiguring_volatile_settings_by_using_driver_verifier_manager__windows2kspanconfiguring-volatile-settings-by-using-driver-verifier-manager-windows-2000"></a><span id="configuring_volatile_settings_by_using_driver_verifier_manager__windows2K"></span><span id="configuring_volatile_settings_by_using_driver_verifier_manager__windows2k"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOWS2K"></span>使用驱动程序验证器管理器 (Windows 2000) 配置易失性设置

**更改易失性设置**

1.  单击 " **可变设置** " 选项卡。

2.  若要启用功能，请选择 " (" 复选 ") 功能的复选框。

3.  若要禁用功能，请清除 ) 复选框 ( "取消选中"。

4.  单击“应用”以应用更改。

驱动程序验证程序管理器显示当前生效的驱动程序验证程序选项，包括易失性设置，但不包括计划在下次重新启动后生效的永久设置的更改。 每个驱动程序都将列出其状态。

### <a name="span-idconfiguring_volatile_settings_by_using_driver_verifier_manager__windowspanspan-idconfiguring_volatile_settings_by_using_driver_verifier_manager__windowspanconfiguring-volatile-settings-by-using-driver-verifier-manager-windows-xp-and-later"></a><span id="configuring_volatile_settings_by_using_driver_verifier_manager__window"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOW"></span>使用驱动程序验证器管理器 (Windows XP 和更高版本配置易失性设置) 

**查看当前处于活动状态的驱动程序验证程序功能或更改易失性设置**

1.  启动驱动程序验证器管理器并选择 " **显示有关当前已验证驱动程序的信息** " 任务。

2.  单击 **“下一步”** 。

    此屏幕显示当前生效的驱动程序验证程序选项，包括易失性设置，但不包括计划在下次重新启动后生效的永久设置的更改。 每个驱动程序都将列出其状态。

3.  若要更改活动的选项，请单击 " **更改**"。 选择或清除所需的选项，然后单击 **"确定"**。

4.  若要验证新的驱动程序，请单击 " **添加**"。 这将打开一个对话框，你可以在其中浏览计算机以查找要验证的驱动程序文件。 找到正确的驱动程序后，单击 " **打开** " 以将其添加到经验证的驱动程序列表中。

5.  若要从列表中删除驱动程序，请选择该驱动程序的名称，然后单击 " **删除**"。

6.  查看完 "驱动程序验证程序" 选项后，或在完成更改后，单击 " **下一步** " 两次，然后单击 " **完成**"。

### <a name="span-iddriver_status_valuesspanspan-iddriver_status_valuesspandriver-status-values"></a><span id="driver_status_values"></span><span id="DRIVER_STATUS_VALUES"></span>驱动程序状态值

驱动程序验证程序管理器为 **当前设置和已验证驱动程序** 上显示的驱动程序显示三个可能的状态值) 屏幕 (运行时信息。 可能的状态值如下：

<span id="Loaded"></span><span id="loaded"></span><span id="LOADED"></span>**时装**  
当前已加载驱动程序，正在验证该驱动程序。

<span id="Unloaded"></span><span id="unloaded"></span><span id="UNLOADED"></span>**接**  
自上一次启动后，该驱动程序至少加载并验证一次，但当前未加载。

<span id="Never_Loaded"></span><span id="never_loaded"></span><span id="NEVER_LOADED"></span>**从未加载**  
已指示驱动程序验证器验证此驱动程序，但自此请求以来尚未加载该驱动程序。 这可能表示该驱动程序是按需加载的，在此会话中尚未需要。 它也可能表示请求了不存在的驱动程序以进行验证，或者驱动程序图像文件已损坏。

### <a name="span-iddisplaying_volatile_settings_by_using_driver_verifier_manager__windowsspanspan-iddisplaying_volatile_settings_by_using_driver_verifier_manager__windowsspandisplaying-volatile-settings-by-using-driver-verifier-manager-windows-2000"></a><span id="displaying_volatile_settings_by_using_driver_verifier_manager__windows"></span><span id="DISPLAYING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOWS"></span>使用驱动程序验证器管理器显示易失性设置 (Windows 2000) 

若要查看当前处于活动状态的驱动程序验证程序功能，请选择 " **驱动程序状态** " 或 " **可变设置** " 选项卡。

其中每个屏幕都显示当前生效的驱动程序验证程序选项，包括易失性设置，但不包括计划在下次重新启动后生效的永久设置的更改。 每个驱动程序都将列出其状态。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**驱动程序验证程序命令语法**](verifier-command-line.md)

[控制驱动程序验证程序](controlling-driver-verifier.md)

 

 






