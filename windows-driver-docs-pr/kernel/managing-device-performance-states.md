---
title: 管理设备性能状态
description: 管理设备性能状态
ms.assetid: 5a4cc09a-e86e-4e5a-98b2-0351b253b5b6
keywords:
- 电源管理 WDK 内核，设备性能状态
- 设备性能状态 WDK 电源管理
- 性能状态 WDK 电源管理
- 自定义电源设置 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2d23d696bb73733dc094b9b8bf0602f56a9c98a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184445"
---
# <a name="managing-device-performance-states"></a>管理设备性能状态


Windows Vista 的功能增强了电源管理基础结构，使驱动程序堆栈可以更好地管理其设备的电源策略。 可以注册驱动程序，以便在系统定义的电源设置更改或系统电源事件发生时获得通知。 设备电源策略所有者可以使用这些通知来适当调整其设备的电源使用情况。 此外，还可以创建自定义电源设置，以提供对特定于设备的电源和性能功能的访问，这些功能可紧密集成到系统电源策略中。 下面是将设备性能状态与系统电源策略集成的两种主要方法。

[为设备创建自定义电源设置](#creating-custom-power-settings-for-a-device)

[注册以通知对活动电源方案、电源方案个人或电源的更改](#registering-to-be-notified-of-a-change-to-the-active-power-scheme)

### <a name="creating-custom-power-settings-for-a-device"></a><a href="" id="creating-custom-power-settings-for-a-device"></a> 为设备创建自定义电源设置

你可以定义可用于配置设备性能状态或节能行为的自定义电源设置。 有关自定义电源设置的信息由电源管理器保存和管理。 系统中的其他组件（如设备驱动程序、服务或应用程序）可以注册，以便在自定义电源设置的值更改时收到通知。 一般情况下，可以使用功率消耗来权衡性能的设备应具有相应的自定义电源设置。 创建自定义电源设置是最灵活的方法，可与系统电源策略紧密集成功率消耗，并提供以下附加优势：

-   自定义用户界面无需使用户能够访问自定义电源设置。 在 "**电源选项**" 控制面板的 "**高级设置**" 页上，所有电源设置（包括自定义电源设置）都将显示给用户。

-   用户和系统管理员可以使用 Powercfg.exe （电源管理命令行工具）轻松编写自定义电源设置的配置脚本。

-   系统管理员也可以选择创建管理模板 (。ADM) 文件，用于对新电源设置进行基于组策略的配置。

单个电源设置包含唯一标识、命名、描述和提供电源设置的值所需的所有信息。 每个电源设置都定义了 GUID、设置名称、描述和 AC 和 DC 电源方案的默认设置。 可以通过使用 [**INF AddPowerSetting 指令**](../install/inf-addpowersetting-directive.md)或动态地为设备创建自定义电源设置，方法是调用随 Microsoft Windows SDK 文档提供的电源管理引用中包含的 Win32 电源管理功能。

驱动程序调用 [**PoRegisterPowerSettingCallback**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterpowersettingcallback) 来注册一个回调例程，该例程由电源管理器调用以通知驱动程序电源设置的更改。 设置更改时，电源管理器将调用回调例程并传递新的设置值。 然后，驱动程序可以执行适用于电源设置的操作。 每个设置由电源设置的 GUID 标识。 在 Wdm .h 和 Ntpoapi 中定义了系统定义的电源设置 Guid。

例如，要在打开或关闭监视器电源时获得通知，驱动程序将调用 **PoRegisterPowerSettingCallback**，并提供标识监视器电源设置 (guid \_ 监视器开机) 的 guid \_ ， \_ 以及一个指向当监视器电源设置的值更改时，电源管理器调用的回调例程的指针。

### <a name="registering-to-be-notified-of-a-change-to-the-active-power-scheme-power-scheme-personality-or-power-source"></a><a href="" id="registering-to-be-notified-of-a-change-to-the-active-power-scheme"></a>注册以通知对活动电源方案、电源方案个人或电源的更改

活动电源方案的个性为用户提供系统整体节能行为的意图。 每个电源方案（包括自定义方案）都有一个指示方案整体意图的个性。 这样，就可以创建更多的自定义电源方案，同时还能提供了解方案意图的所有好处。 Windows Vista 包含以下三个系统定义的电源方案及其相应的个性。

<a href="" id="maximum-power-savings"></a>**最大节能**  
降低性能以最大程度地降低功率消耗。

<a href="" id="automatic--balanced-"></a>**自动 (平衡) **  
允许系统基于整体功率消耗选择最佳电源状态级别。

<a href="" id="maximum-performance-------"></a>**最高性能**   
提供最大性能，而不考虑功率消耗。

电源可以是交流或直流电电源。

设备电源策略所有者可以使用有关活动电源方案、电源方案个性和电源的信息来调整设备电源策略。 例如，如果电源方案的个人设置更改为 **最大节能**，则设备电源策略所有者可能会主动关闭设备电源。 但是，如果电源方案的 "个人" 设置更改为 " **最大性能**"，则设备电源策略所有者可能会保持其设备的性能级别，而不是减少功率消耗，并可能始终保持设备的电源状态，以确保最高的性能级别。

可以注册一个驱动程序，以便在发生更改时通知活动电源方案、电源方案的个性或电源。 驱动程序调用 **PoRegisterPowerSettingCallback** 来注册电源管理器调用的回调例程，以通知驱动程序此类更改，如下所示：

-   若要注册活动电源方案的更改通知，请提供表示电源方案 (GUID \_ active POWERSCHEME) 设置的 guid \_ 。 当活动电源方案发生变化时，电源管理器将调用回调例程，即使新的电源方案的个性相同也是以前的电源方案。

-   若要注册对电源方案个人更改的通知，请提供表示电源方案个性 (GUID \_ POWERSCHEME 个性) 设置的 GUID \_ 。 只要活动的电源方案发生变化并且新的电源方案的个性不同于以前的电源方案的个性，电源管理器就会调用回调例程。

-   若要注册对 power 源的更改的通知，请提供表示电源 (GUID \_ ACDC \_ power source) 设置的 guid \_ 。 然后，在电源设置发生更改时，电源管理器将调用回调例程。

当活动电源方案更改或电源方案的个性变化时，电源管理器会调用回调例程，并传递表示新电源方案或电源方案个性的 GUID。 然后，驱动程序可以执行适用于更改的操作。

"活动的电源方案设置" 和 "电源方案个人设置" 使用以下 Guid 来标识其各自的值：

-   GUID \_ 最大节能 \_ \_ ，对应于 **最大节能** 电源方案及其相应的个性。

-   最 \_ 小 \_ 功率 \_ 节省，对应于 **最大性能** 电源方案及其相应的个性。

-   GUID \_ 典型 \_ 节能 \_ ，对应于 **自动 (平衡) ** 电源方案及其相应的个性。

当电源发生变化时，电源管理器会调用回调例程，并传递表示 "电源源" 设置的 GUID 和 "电源源" 设置的值，此值指示计算机是否由交流电源、直流电源或短期直流电电源提供支持。

 

