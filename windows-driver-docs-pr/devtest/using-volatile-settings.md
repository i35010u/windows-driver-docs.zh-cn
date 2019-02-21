---
title: 使用易失性设置
description: 使用易失性设置
ms.assetid: 16fb8c2a-60d8-4c0a-879d-447a1cda5415
keywords:
- 驱动程序验证程序 WDK，易失性设置
- 易失性设置 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1aa9c074a96f4da35f7e0b366c7dbfa43117c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521474"
---
# <a name="using-volatile-settings"></a>使用易失性设置


## <span id="ddk_using_volatile_settings_tools"></span><span id="DDK_USING_VOLATILE_SETTINGS_TOOLS"></span>


仅当重新启动计算机 （"重启"） 时，对驱动程序验证程序的状态 （激活、 停用、 更改选项，或更改正在验证的驱动程序的列表） 的大多数更改才能生效。

但是，可以激活和停用不重启的一些选项。 这些称为*易失性的设置。* 更改这些设置将立即生效，并持续直到下一步启动，或再次更改它们。

本部分说明的易失性的设置以及如何使用它们的驱动程序验证程序包括在不同版本的 Windows 版本上。

### <a name="span-idchangingoptionswithoutrebootingspanspan-idchangingoptionswithoutrebootingspanchanging-options-without-rebooting"></a><span id="changing_options_without_rebooting"></span><span id="CHANGING_OPTIONS_WITHOUT_REBOOTING"></span>更改选项，但未重新启动

可以激活和停的所有驱动程序验证程序选项，用除外[DDI 符合性检查](ddi-compliance-checking.md)，[电源框架延迟模糊](concurrency-stress-test.md)， [Storport 验证](dv-storport-verification.md)，[SCSI 验证](scsi-verification.md)并[磁盘完整性检查](disk-integrity-checking.md)，而无需重启计算机。

**请注意**  上的 Windows Vista 之前的 Windows 版本中，你可以激活和停用而无需重启计算机的仅以下 Driver Verifier 选项。 但是，若要执行此操作，驱动程序验证程序必须已在运行，也就是说，必须使用至少一个选项启动驱动程序验证程序，然后重新启动计算机。 它运行后，你可以激活和停用而无需额外的重新启动这些设置。
-   [特殊的池](special-pool.md)

-   [强制 IRQL 检查](force-irql-checking.md)

-   [资源不足模拟](low-resources-simulation.md)

 

### <a name="span-idchangingdriverswithoutrebootingspanspan-idchangingdriverswithoutrebootingspanchanging-drivers-without-rebooting"></a><span id="changing_drivers_without_rebooting"></span><span id="CHANGING_DRIVERS_WITHOUT_REBOOTING"></span>更改驱动程序，但未重新启动

从 Windows Vista 开始，可以添加和删除驱动程序 （即，启动和停止验证的驱动程序） 而无需重启计算机，即使驱动程序验证程序尚未运行。

你还可以启动的驱动程序，而无需重新启动，已加载的验证，但无法而不必重新启动停止的已加载的驱动程序验证。 加载驱动程序和进行验证，驱动程序验证工具监视它直到下次重新启动，但你可以关闭后可选驱动程序验证程序将检查驱动程序而无需重新启动，因此可尽量减少驱动程序验证程序开销。

在 Windows XP 和 Windows Server 2003 中，可以添加和删除驱动程序而无需重新启动，但仅当驱动程序当前未加载。

可以使用更改的易失性设置[**验证程序命令行**](verifier-command-line.md)，或驱动程序验证程序管理器。 有两个版本的驱动程序验证程序管理器-一个用于[Windows 2000](driver-verifier-manager--windows-2000-.md) ，另一个用于[Windows XP 及更高版本](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idvolatileandregistrysettingsspanspan-idvolatileandregistrysettingsspanvolatile-and-registry-settings"></a><span id="volatile_and_registry_settings"></span><span id="VOLATILE_AND_REGISTRY_SETTINGS"></span>易失性和注册表设置

能够添加和更改驱动程序以及无需重新启动设置选项十分显著方便，并且它允许你在某些测试方案中，否则是不可能运行驱动程序验证程序。

但是，因为有几种好处将驱动程序验证程序设置添加到注册表的传统模型，您需要为每个设置决定是否想要使用易失性的方法，或将其设置在注册表中，或两者中。

-   易失性或"运行时"设置立即生效，但在关闭或重新启动 Windows 时，这些设置会丢失。

-   注册表设置需要重新启动，但它们保留在注册表中进行更改并再次重新启动之前。

应设置一致地使用或需要度量时加载驱动程序添加到注册表。 在需要时，可以启用其他设置。

使用注册表设置和易失性设置时，请记住，而不是注册表设置; 使用易失性设置它们不是新增内容。

### <a name="span-idconfiguringvolatilesettingsbyusingtheverifiercommandlinespanspan-idconfiguringvolatilesettingsbyusingtheverifiercommandlinespanconfiguring-volatile-settings-by-using-the-verifier-command-line"></a><span id="configuring_volatile_settings_by_using_the_verifier_command_line"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_THE_VERIFIER_COMMAND_LINE"></span>通过使用验证程序命令行配置易失性设置

若要添加或删除易失性的选项，请使用 **/volatile /flags**参数。

(Windows XP 及更高版本)若要添加或删除驱动程序从易失性的列表，请使用 **/volatile /adddriver**或 **/volatile /removedriver**参数。 请参阅[**驱动程序验证工具的命令语法**](verifier-command-line.md)有关详细信息。

-   若要启动或停止时避免重新启动的驱动程序的验证：

    ```
    verifier /volatile /adddriver DriverName.sys
    verifier /volatile /removedriver DriverName.sys
    ```

    您可以使用此命令语法来添加 （启动验证） 的任何驱动程序，甚至是当前加载的驱动程序。 命令为删除 （停止验证） 的当前加载的驱动程序将失败。 如往常一样，未加载的驱动程序的验证将开始加载该驱动程序。

-   若要激活或停用不重启的选项：

    ```
    verifier /volatile /flags Options
    ```

    您可以使用任何 Driver Verifier 选项后，此命令语法除外[SCSI 验证](scsi-verification.md)并[磁盘完整性检查](disk-integrity-checking.md)。 例如，

    ```
    verifier /volatile /flags 0x20
    ```

    此命令将激活[死锁检测](deadlock-detection.md)选项而无需重新启动。

-   若要关闭所有驱动程序验证程序选项：

    无法停止而不必重新启动当前加载的驱动程序验证。 但是，您可以使用以下命令语法停用的所有驱动程序验证程序选项而无需重新启动，从而开销降到最低直到下次重新启动。

    ```
    verifier /volatile /flags 0
    ```

    继续监视使用中的选项的驱动程序的 driver Verifier[自动检查](automatic-checks.md)功能，这不能已关闭，但开销减少到大约 10%的典型验证的开销。

### <a name="span-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindows2kspanspan-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindows2kspanspan-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindows2kspanconfiguring-volatile-settings-by-using-driver-verifier-manager-windows-2000"></a><span id="configuring_volatile_settings_by_using_driver_verifier_manager__windows2K"></span><span id="configuring_volatile_settings_by_using_driver_verifier_manager__windows2k"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOWS2K"></span>通过使用驱动程序验证程序管理器 (Windows 2000) 配置易失性设置

**若要更改的易失性设置**

1.  单击**易失性设置**选项卡。

2.  若要启用一项功能，请选择一项功能 （"检查"） 复选框。

3.  若要禁用一项功能，请清除 （"取消选中"） 复选框。

4.  单击“应用”以应用更改。

驱动程序验证程序管理器显示的 Driver Verifier 选项当前有效，包括易失性设置，但不是包括更改到永久性设置，计划在下一步的重启后才会生效。 每个驱动程序将列出其状态。

### <a name="span-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindowspanspan-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindowspanconfiguring-volatile-settings-by-using-driver-verifier-manager-windows-xp-and-later"></a><span id="configuring_volatile_settings_by_using_driver_verifier_manager__window"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOW"></span>配置易失性设置通过使用驱动程序验证程序管理器 (Windows XP 及更高版本)

**若要查看当前处于活动状态的驱动程序验证程序功能或更改的易失性设置**

1.  启动驱动程序验证程序管理器，然后选择**显示有关当前已验证的驱动程序信息**任务。

2.  单击“下一步” 。

    此屏幕显示的 Driver Verifier 选项当前有效，包括易失性设置，但不是包括更改到永久性设置，计划在下一步的重启后才会生效。 每个驱动程序将列出其状态。

3.  若要更改活动的选项，请单击**更改**。 选择或清除所需的选项，然后单击**确定**。

4.  若要验证新的驱动程序，请单击**添加**。 这将打开一个对话框，您可以在其中浏览你想要验证的驱动程序文件的计算机。 找到后正确的驱动程序，单击**打开**将其添加到已验证的驱动程序的列表。

5.  若要从列表中删除驱动程序，选择该驱动程序的名称，然后单击**删除**。

6.  完成后查看 Driver Verifier 选项生效时，或者当你已完成更改后，单击**下一步**两次，然后单击**完成**。

### <a name="span-iddriverstatusvaluesspanspan-iddriverstatusvaluesspandriver-status-values"></a><span id="driver_status_values"></span><span id="DRIVER_STATUS_VALUES"></span>驱动程序状态的值

驱动程序验证程序管理器显示的驱动程序上显示的三个可能状态值**当前设置和已验证的驱动程序 （运行时信息）** 屏幕。 可能的状态值如下所示：

<span id="Loaded"></span><span id="loaded"></span><span id="LOADED"></span>**加载**  
驱动程序当前已加载，正在被验证。

<span id="Unloaded"></span><span id="unloaded"></span><span id="UNLOADED"></span>**卸载**  
该驱动程序已加载，并从上次启动以来至少一次验证但当前不是加载。

<span id="Never_Loaded"></span><span id="never_loaded"></span><span id="NEVER_LOADED"></span>**永远不加载**  
驱动程序验证程序已指示若要验证此驱动程序，但此请求之后尚未加载该驱动程序。 这可能指示驱动程序是按需加载并不尚未只需在此会话中。 它还可能指示不存在的驱动程序已请求进行验证，或驱动程序图像文件已损坏。

### <a name="span-iddisplayingvolatilesettingsbyusingdriververifiermanagerwindowsspanspan-iddisplayingvolatilesettingsbyusingdriververifiermanagerwindowsspandisplaying-volatile-settings-by-using-driver-verifier-manager-windows-2000"></a><span id="displaying_volatile_settings_by_using_driver_verifier_manager__windows"></span><span id="DISPLAYING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOWS"></span>使用驱动程序验证程序管理器 (Windows 2000) 显示易失性设置

若要查看当前处于活动状态的驱动程序验证程序功能，请选择**驱动程序状态**或**易失性设置**选项卡。

每个这些屏幕显示的 Driver Verifier 选项当前有效，包括易失性设置，但不是包括更改到永久性设置，计划在下一步的重启后才会生效。 每个驱动程序将列出其状态。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[**驱动程序验证工具的命令语法**](verifier-command-line.md)

[控制驱动程序验证程序](controlling-driver-verifier.md)

 

 






