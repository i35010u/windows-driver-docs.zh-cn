---
title: UWP 设备应用的自动安装
description: 本主题介绍如何进行自动安装，以及如何更新和卸载应用、元数据和驱动程序。
ms.assetid: ED9C7A63-5D2A-45D3-AD62-32C6876142FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 332a9277cad1f60cd142b226f3e302e6f17db89a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387955"
---
# <a name="automatic-installation-for-uwp-device-apps"></a>UWP 设备应用的自动安装


在 Windows 8.1 设备制造商可以配置当用户将其设备连接到 PC 时自动安装其 UWP 设备应用。 本主题介绍如何进行自动安装，以及如何更新和卸载应用、元数据和驱动程序。 有关设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**  务必要考虑，自动安装功能不提供通知给用户安装应用。 有些用户可能发现这种体验让人困惑和令人沮丧，并为您的应用程序提供错误评级。

 

指定设备应用的包中的详细信息时启用了自动安装**UWP 设备应用**一部分**应用信息**页**设备元数据创建向导**. 有关详细信息，请参阅[步骤 2:创建设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idacquisitionoverviewspanspan-idacquisitionoverviewspanspan-idacquisitionoverviewspanacquisition-overview"></a><span id="Acquisition_overview"></span><span id="acquisition_overview"></span><span id="ACQUISITION_OVERVIEW"></span>获取概述


可以通过三种方式之一中的用户来获得 UWP 设备应用：

-   **自动安装**:应用会自动获取并安装外围设备连接到 PC 的第一个时间。 这是安装的 UWP 设备应用程序的最常见方式。
-   **手动安装**:用户在 Microsoft Store 中找到的应用程序，并从该处安装它。 这通常是如何安装应用更新和其他 UWP 应用。
-   **OEM 预安装**:适用于 PC 内部设备或系统组件的应用可以通过新的 PC 的一部分的 OEM 预安装。 有关详细信息，请参阅[预安装应用程序使用 DISM](https://go.microsoft.com/fwlink/p/?LinkId=325524)。

**请注意**  UWP 应用的 PC 内部设备的设备应用程序均不适合自动安装。 只能通过手动安装和 OEM 将获得预安装。

 

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


为了使自动安装正常工作，用户需要：

-   选择加入**建议的设置**Windows 安装过程。

-   登录到 Microsoft Store。

-   处于联机状态。

这样，Windows 会自动获取元数据、 应用和驱动程序 （如果需要）。 如果没有 Internet 连接不可用，自动安装会在更高版本时，当它可以访问 Internet。

## <a name="span-idhowautomaticinstallationworksspanspan-idhowautomaticinstallationworksspanspan-idhowautomaticinstallationworksspanhow-automatic-installation-works"></a><span id="How_automatic_installation_works"></span><span id="how_automatic_installation_works"></span><span id="HOW_AUTOMATIC_INSTALLATION_WORKS"></span>自动安装的工作方式


![为自动安装的四个步骤： 连接设备，设备元数据下载、 设备驱动程序下载 （如适用）、 应用程序下载](images/autoinstallbehindscenes.png)

有四个阶段自动安装到：

1.  **设备连接**:当在设备接通电源或与电脑配对的时 Windows 会从 Windows 元数据和 Internet 服务 (WMIS) 请求的设备元数据并根据需要从 Windows 更新的设备驱动程序。

2.  **下载设备元数据**:Windows 从 WMIS 下载设备元数据和分析来识别与设备相关联的应用。 这会触发应用的下载。

3.  **设备驱动程序下载**:如果需要驱动程序，Windows 将从 Windows 更新下载这些，并自动安装它们。

4.  **安装设备应用**:Windows 下载该应用程序并安装到**所有应用**当前登录的用户的屏幕。

如果有任何这些步骤时出现错误，用户将看到一条错误消息，有关**设备**页**设置**应用。

### <a name="span-idifthereisnointernetconnectionspanspan-idifthereisnointernetconnectionspanspan-idifthereisnointernetconnectionspanif-there-is-no-internet-connection"></a><span id="If_there_is_no_Internet_connection"></span><span id="if_there_is_no_internet_connection"></span><span id="IF_THERE_IS_NO_INTERNET_CONNECTION"></span>如果没有 Internet 连接

如果 PC 未连接到 Internet，或按流量计费的连接，Windows 将等待以执行自动安装。 下一次 PC 具有不受限制的 Internet 连接，Windows 将自动重试。 在后台，而不会中断用户以无提示方式执行安装。

### <a name="span-idiftheuserisnotloggedintothewindowsstorespanspan-idiftheuserisnotloggedintothewindowsstorespanspan-idiftheuserisnotloggedintothewindowsstorespanif-the-user-is-not-logged-into-the-microsoft-store"></a><span id="If_the_user_is_not_logged_into_the_Windows_Store"></span><span id="if_the_user_is_not_logged_into_the_windows_store"></span><span id="IF_THE_USER_IS_NOT_LOGGED_INTO_THE_WINDOWS_STORE"></span>如果用户未登录到 Microsoft Store

如果用户未登录到 Microsoft 帐户与 Microsoft Store，Windows 将等待以执行自动安装。 下次用户登录到 Microsoft Store 使用 Microsoft 帐户时，Windows 将自动重试。 在后台，而不会中断用户以无提示方式执行安装。

## <a name="span-idupdatingdevicedriversspanspan-idupdatingdevicedriversspanspan-idupdatingdevicedriversspanupdating-device-drivers"></a><span id="Updating_device_drivers"></span><span id="updating_device_drivers"></span><span id="UPDATING_DEVICE_DRIVERS"></span>更新设备驱动程序


驱动程序更新的通过 Windows 更新分配作为可选更新，只要用户选择在从 Windows Update 接收更新。 如果用户已完成设备安装程序，并且已获取元数据和安装驱动程序，驱动程序更新不会自动分发到设备。

驱动程序更新不会耦合到应用更新，因此驱动程序更新应旨在确保与现有应用程序兼容性。 如果 Windows 更新，请通过分发的驱动程序更新，或者用户手动重新安装或更新驱动程序，应用应适当地处理这。 如果你的应用使用自定义驱动程序，请务必维护兼容性和功能的协定。 有关详细信息，请参阅[UWP 设备应用程序的内部设备](uwp-device-apps-for-specialized-devices.md)。

## <a name="span-idupdatingdevicemetadataspanspan-idupdatingdevicemetadataspanspan-idupdatingdevicemetadataspanupdating-device-metadata"></a><span id="Updating_device_metadata"></span><span id="updating_device_metadata"></span><span id="UPDATING_DEVICE_METADATA"></span>更新设备元数据


可以更新由 WMIS 分发的元数据，以指向新的或不同的 UWP 设备应用。 大约 8 到 15 天后的更新的元数据，该值指示新的应用程序，提交的连接，并为第一次设置新设备将收到新应用程序。 但是，新的应用程序中更新的元数据指示未自动分发到为其设备安装程序已完成，因为用户以前接收设备的设备元数据的电脑。

UWP 设备应用会自动下载仅一次，当设备在最初设置。 如果设备元数据更新为指向不同的应用，旧的应用应该播发到用户，新建一个，以便用户可以获取它从 Microsoft Store 手动。 最后，应从 Microsoft Store 中删除旧的应用。 用户还可以通过转到获取到新的应用**设备**页上**设置**应用程序并单击**看到应用**为该设备的链接。

**针对添加的特别说明特别访问权**:如果较新的元数据授予 UWP 设备应用特权访问 （如果之前不存在访问） 的设备，，提交你的元数据时间至少为 20 天之前提交您的应用程序。 新的元数据将适用于新用户 8 到 15 天后提交。 然后，将应用更新发布到 Microsoft Store。 当用户获取应用更新，假设用户更新任何所需的驱动程序时，该应用程序将具有特权访问设备。

## <a name="span-idupdatingdeviceappsspanspan-idupdatingdeviceappsspanspan-idupdatingdeviceappsspanupdating-device-apps"></a><span id="Updating_device_apps"></span><span id="updating_device_apps"></span><span id="UPDATING_DEVICE_APPS"></span>正在更新的设备应用程序


由用户，就像任何其他 UWP 应用更新手动触发 UWP 设备应用更新。 Microsoft Store 向用户显示所有可用的应用更新。 用户手动选择更新应用程序。 您应设计应用程序，以与较旧版本的元数据和驱动程序兼容。 设备元数据或驱动程序可能不是最新的应用程序中，因为手动安装从 Microsoft Store 的 UWP 设备应用程序不会自动触发的元数据或驱动程序分发。

## <a name="span-iduninstallingdevicesoftwarespanspan-iduninstallingdevicesoftwarespanspan-iduninstallingdevicesoftwarespanuninstalling-device-software"></a><span id="Uninstalling_device_software"></span><span id="uninstalling_device_software"></span><span id="UNINSTALLING_DEVICE_SOFTWARE"></span>卸载设备软件


独立于 Microsoft Store 应用设备应用程序卸载设备驱动程序和设备元数据。 当用户卸载设备时，驱动程序和元数据自动卸载设备卸载功能的一部分。

UWP 设备应用程序必须由用户手动卸载。 完成后，设备驱动程序和设备元数据不会自动卸载。

 

 





