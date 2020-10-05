---
title: UWP 设备应用的自动安装
description: 本主题介绍如何进行自动安装，以及如何更新和卸载应用、元数据和驱动程序。
ms.assetid: ED9C7A63-5D2A-45D3-AD62-32C6876142FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ce96ebd1c0bd6e0e4da8ca8f76b975563ac2a4e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734483"
---
# <a name="automatic-installation-for-uwp-device-apps"></a>UWP 设备应用的自动安装


在 Windows 8.1 中，设备制造商可以将其 UWP 设备应用配置为在用户将其设备连接到电脑时自动安装。 本主题介绍如何进行自动安装，以及如何更新和卸载应用、元数据和驱动程序。 有关设备应用的详细信息，请参阅 " [满足 UWP 设备应用](meet-uwp-device-apps.md)"。

**注意**   请注意，在安装应用时，自动安装功能不会向用户提供通知。 某些用户可能会发现这种体验令人费解，并使应用程序成为不良评级。

 

当你在**设备元数据创作向导**的 "**应用程序信息**" 页的**UWP 设备应用**部分中指定设备应用包详细信息时，将启用自动安装。 有关详细信息，请参阅 [步骤2：创建设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idacquisition_overviewspanspan-idacquisition_overviewspanspan-idacquisition_overviewspanacquisition-overview"></a><span id="Acquisition_overview"></span><span id="acquisition_overview"></span><span id="ACQUISITION_OVERVIEW"></span>购置概述


用户可以通过以下三种方式之一获取 UWP 设备应用：

-   **自动安装**：第一次将外围设备连接到电脑时，将自动获取并安装该应用。 这是安装了 UWP 设备应用最常见的方式。
-   **手动安装**：用户查找 Microsoft Store 中的应用并从该应用中安装应用。 这通常是应用更新和其他 UWP 应用的安装方式。
-   **Oem 预安装**：适用于电脑内部设备或系统组件的应用可由 OEM 预安装为新 pc 的一部分。 有关详细信息，请参阅 [使用 DISM 预安装应用](/previous-versions/windows/it-pro/windows-8.1-and-8/dn387084(v=win.10))。

**注意**   适用于电脑内部设备的 UWP 设备应用无法进行自动安装。 仅可通过手动安装和 OEM 预安装获取它们。

 

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


若要运行自动安装，用户需要：

-   在 Windows 安装过程中选择 **使用推荐的设置** 。

-   登录到 Microsoft Store。

-   处于联机状态。

这允许 Windows 根据需要) 自动获取元数据、应用和驱动程序 (。 如果没有可用的 Internet 连接，则在以后可以访问 Internet 时，将会进行自动安装。

## <a name="span-idhow_automatic_installation_worksspanspan-idhow_automatic_installation_worksspanspan-idhow_automatic_installation_worksspanhow-automatic-installation-works"></a><span id="How_automatic_installation_works"></span><span id="how_automatic_installation_works"></span><span id="HOW_AUTOMATIC_INSTALLATION_WORKS"></span>自动安装的工作原理


![自动安装的四个步骤：设备连接、设备元数据下载、设备驱动程序下载 (如适用) 、应用下载](images/autoinstallbehindscenes.png)

自动安装分为以下四个阶段：

1.  **设备已连接**：设备接通电源或与电脑配对后，windows 将从 Windows 元数据和 Internet 服务请求设备元数据 (WMIS) ，并根据需要从 Windows 更新中请求设备驱动程序。

2.  **已下载设备元数据**： WINDOWS 从 WMIS 下载设备元数据，并对其进行分析以识别与设备关联的应用。 这会触发应用的下载。

3.  **下载设备驱动程序**：如果需要驱动程序，Windows 将从 Windows 更新下载这些驱动程序并自动安装它们。

4.  **已安装设备应用**： Windows 下载应用并将其安装到当前已登录用户的 " **所有应用** " 屏幕。

如果在任何这些步骤中出现错误，用户将在 "**设置**" 应用的 "**设备**" 页上看到一条错误消息。

### <a name="span-idif_there_is_no_internet_connectionspanspan-idif_there_is_no_internet_connectionspanspan-idif_there_is_no_internet_connectionspanif-there-is-no-internet-connection"></a><span id="If_there_is_no_Internet_connection"></span><span id="if_there_is_no_internet_connection"></span><span id="IF_THERE_IS_NO_INTERNET_CONNECTION"></span>如果没有 Internet 连接

如果电脑未连接到 Internet 或处于按流量计费的连接上，则 Windows 将等待执行自动安装。 下一次电脑具有不受限制的 Internet 连接时，Windows 将自动重试。 在后台无提示执行安装，无需中断用户。

### <a name="span-idif_the_user_is_not_logged_into_the_windows_storespanspan-idif_the_user_is_not_logged_into_the_windows_storespanspan-idif_the_user_is_not_logged_into_the_windows_storespanif-the-user-is-not-logged-into-the-microsoft-store"></a><span id="If_the_user_is_not_logged_into_the_Windows_Store"></span><span id="if_the_user_is_not_logged_into_the_windows_store"></span><span id="IF_THE_USER_IS_NOT_LOGGED_INTO_THE_WINDOWS_STORE"></span>如果用户未登录到 Microsoft Store

如果用户未使用 Microsoft 帐户登录到 Microsoft Store，则 Windows 将等待执行自动安装。 用户下次使用 Microsoft 帐户登录到 Microsoft Store 时，Windows 将自动重试。 在后台无提示执行安装，无需中断用户。

## <a name="span-idupdating_device_driversspanspan-idupdating_device_driversspanspan-idupdating_device_driversspanupdating-device-drivers"></a><span id="Updating_device_drivers"></span><span id="updating_device_drivers"></span><span id="UPDATING_DEVICE_DRIVERS"></span>更新设备驱动程序


只要用户已选择从 Windows 更新接收更新，驱动程序更新将作为可选更新分发到 Windows 更新。 如果用户已完成设备安装并且已经安装了元数据和驱动程序，则驱动程序更新不会自动分发到设备。

驱动程序更新不与应用程序更新耦合，因此应设计驱动程序更新以确保与现有应用程序的兼容性。 如果通过 Windows 更新分发了驱动程序更新，或者用户手动重新安装或更新了驱动程序，则应用程序应相应地处理这种情况。 如果你的应用使用自定义驱动程序，请务必维护兼容性和功能协定。 有关详细信息，请参阅 [内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)。

## <a name="span-idupdating_device_metadataspanspan-idupdating_device_metadataspanspan-idupdating_device_metadataspanupdating-device-metadata"></a><span id="Updating_device_metadata"></span><span id="updating_device_metadata"></span><span id="UPDATING_DEVICE_METADATA"></span>更新设备元数据


可以将 WMIS 分发的元数据更新为指向新的或不同的 UWP 设备应用。 大约需要8到15天后，提交已更新的元数据（表示新应用）后，首次连接和设置的新设备将获取新应用。 但更新的元数据中指示的新应用不会自动分发到已完成设备设置的电脑，因为用户以前已收到设备的设备元数据。

当设备最初设置时，UWP 设备应用仅自动下载一次。 如果将设备元数据更新为指向不同的应用程序，则旧应用程序应向用户公布新的应用程序，以便用户可以手动从 Microsoft Store 获取该应用程序。 最终，应从 Microsoft Store 中删除旧应用。 用户还可以通过转到 "**设置**" 应用上的 "**设备**" 页并单击该设备的 "**获取应用程序**" 链接来访问新应用程序。

**添加特权访问的特殊说明**：如果更新的元数据授予 UWP 设备应用对设备的特权访问权限 (在) 之前没有访问权限，请在提交应用之前至少20天提交元数据。 新的元数据将在提交后8-15 天可用。 然后，将应用程序更新发布到 Microsoft Store。 如果用户获取应用更新，假设用户更新了任何所需的驱动程序，则该应用将具有对设备的特权访问权限。

## <a name="span-idupdating_device_appsspanspan-idupdating_device_appsspanspan-idupdating_device_appsspanupdating-device-apps"></a><span id="Updating_device_apps"></span><span id="updating_device_apps"></span><span id="UPDATING_DEVICE_APPS"></span>更新设备应用


UWP 设备应用更新由用户手动触发，就像任何其他 UWP 应用更新一样。 Microsoft Store 向用户显示所有可用的应用更新。 用户手动选择更新应用程序。 应该将应用程序设计为与较旧的元数据和驱动程序兼容。 此设备的元数据或驱动程序可能不是最新的应用程序，因为从 Microsoft Store 手动安装 UWP 设备应用程序不会自动触发元数据或驱动程序的分发。

## <a name="span-iduninstalling_device_softwarespanspan-iduninstalling_device_softwarespanspan-iduninstalling_device_softwarespanuninstalling-device-software"></a><span id="Uninstalling_device_software"></span><span id="uninstalling_device_software"></span><span id="UNINSTALLING_DEVICE_SOFTWARE"></span>正在卸载设备软件


设备驱动程序和设备元数据独立于 Microsoft Store 设备应用进行卸载。 当用户卸载设备时，只会在设备卸载过程中自动卸载驱动程序和元数据。

UWP 设备应用必须由用户手动卸载。 完成此操作后，不会自动卸载设备驱动程序和设备元数据。

 

