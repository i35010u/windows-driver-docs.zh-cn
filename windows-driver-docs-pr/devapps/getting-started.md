---
title: UWP 设备应用入门
description: 从这里开始构建 UWP 设备应用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47dbdbb8a1e2a4644e5b006f74be7f574ce200e4
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124187"
---
# <a name="getting-started-with-uwp-device-apps"></a>UWP 设备应用入门


从这里开始构建 UWP 设备应用。

![windows 应用商店设备应用入门](images/devices-diagram-350x350.png)

设备制造商可以创建用作设备配套的 UWP 设备应用。 UWP 设备应用的功能超出常规的 UWP 应用，可执行特权操作，例如固件更新。 而且，UWP 设备应用程序可以从自动播放 (在更多设备上启动，而不能) 、首次连接设备时自动安装，并扩展 Windows 中内置的打印机和照相机体验。

**注意**  Windows 运行时设备 Api 不需要设备元数据。 这意味着你的应用程序无需成为 UWP 设备应用即可使用它们。 UWP 应用可以使用这些 Api 来访问 USB、人体学接口设备 (HID) 、Bluetooth 设备等。 有关详细信息，请参阅 [集成设备](/previous-versions/windows/apps/dn263141(v=win.10))。

 

若要了解 UWP 移动宽带应用，请参阅 [Mobile Broadband](../mobilebroadband/index.md)（移动宽带）。

## <a name="span-id1_get_set_upspanspan-id1_get_set_upspan1-get-set-up"></a><span id="1._get_set_up"></span><span id="1._GET_SET_UP"></span>1. 获取设置


若要开发 UWP 设备应用：需要 Microsoft Visual Studio、开发 UWP 应用以及设备元数据创作向导来开发设备元数据。

**注意**  若要在 Windows 10 中开发 UWP 设备应用，请 (WDK) Microsoft Visual Studio 下载2017和 Windows 驱动程序工具包。 [成为 Windows 有问必答，获取工具包和工具](https://go.microsoft.com/fwlink/p/?LinkId=526775)

 

### <a name="span-idif_you_re_also_developing_driversspanspan-idif_you_re_also_developing_driversspanspan-idif_you_re_also_developing_driversspanif-youre-also-developing-drivers"></a><span id="If_you_re_also_developing_drivers"></span><span id="if_you_re_also_developing_drivers"></span><span id="IF_YOU_RE_ALSO_DEVELOPING_DRIVERS"></span>如果还在开发驱动程序

如果要开发 Windows 驱动程序以及 UWP 设备应用，请使用 Microsoft Visual Studio Professional 或 Microsoft Visual Studio Ultimate 来创建 UWP 设备应用。 这些版本包括新的设备元数据创作向导，Windows 驱动程序工具包也需要该向导 (WDK) 8.1。

1.  [下载 Visual Studio Professional 或 Visual Studio Ultimate](https://go.microsoft.com/fwlink/p/?LinkId=302196)
2.  [下载 WDK 8。1](https://go.microsoft.com/fwlink/p/?LinkId=302196)

### <a name="span-idif_you_re_not_going_to_be_developing_driversspanspan-idif_you_re_not_going_to_be_developing_driversspanspan-idif_you_re_not_going_to_be_developing_driversspanif-youre-not-going-to-be-developing-drivers"></a><span id="If_you_re_not_going_to_be_developing_drivers"></span><span id="if_you_re_not_going_to_be_developing_drivers"></span><span id="IF_YOU_RE_NOT_GOING_TO_BE_DEVELOPING_DRIVERS"></span>如果不打算开发驱动程序

如果不需要开发驱动程序，可以使用适用于 Windows 的 Microsoft Visual Studio Express 2015 来创建 UWP 设备应用。 但此版本的 Visual Studio 安装不包括设备元数据创作向导的 SDK 版本。 若要获取新的设备元数据创作向导，还必须下载独立 Windows 8.1 SDK。

1.  [下载适用于 Windows 10 的 Visual Studio Express 2015](https://visualstudio.microsoft.com/vs/express/)
2.  [下载独立 Windows 8.1 SDK](https://go.microsoft.com/fwlink/p/?LinkId=302196)

## <a name="span-id2_build_some_regular_windows_store_appsspanspan-id2_build_some_regular_windows_store_appsspan2-build-some-regular-uwp-apps"></a><span id="2._build_some_regular_windows_store_apps"></span><span id="2._BUILD_SOME_REGULAR_WINDOWS_STORE_APPS"></span>2. 生成一些常规 UWP 应用


UWP 设备应用是一种特殊类型的 UWP 应用。 因此，在开发第一个 UWP 设备应用之前，请设置生成一些常规 UWP 应用。

-   [注册-注册 Microsoft Store 开发人员帐户](https://go.microsoft.com/fwlink/p/?LinkId=302197)
-   [Microsoft Visual Studio 入门](/previous-versions/windows/apps/br211384(v=win.10))
-   请参阅 [Microsoft Store 设计原则](/windows/uwp/design/)

## <a name="span-id3_learn_what_makes_windows_store_device_apps_specialspanspan-id3_learn_what_makes_windows_store_device_apps_specialspan3-learn-what-makes-uwp-device-apps-special"></a><span id="3._learn_what_makes_windows_store_device_apps_special"></span><span id="3._LEARN_WHAT_MAKES_WINDOWS_STORE_DEVICE_APPS_SPECIAL"></span>3. 了解如何实现 UWP 设备应用的特殊功能


了解可以对 UWP 设备应用执行的特殊操作以及生成该应用所要执行的操作。

-   [初识 UWP 设备应用](meet-uwp-device-apps.md)
-   [构建 UWP 设备应用](the-workflow.md)

## <a name="span-id4_download_samplesspanspan-id4_download_samplesspan4-download-samples"></a><span id="4._download_samples"></span><span id="4._DOWNLOAD_SAMPLES"></span>4. 下载示例


可以在示例库中找到设备相关的示例以及 [设备和传感器](/samples/browse/) 关键字。 了解如何在完整示例的上下文中使用 Api。 可以告诉 UWP 设备应用，因为它包含一个将其与设备元数据关联的 StoreManifest.xml 文件。 这些示例用 [UWP 设备应用](/samples/browse/) 关键字进行标记。

## <a name="span-id4_build_your_own_windows_store_device_appspanspan-id4_build_your_own_windows_store_device_appspan4-build-your-own-uwp-device-app"></a><span id="4._build_your_own_windows_store_device_app"></span><span id="4._BUILD_YOUR_OWN_WINDOWS_STORE_DEVICE_APP"></span>4. 构建你自己的 UWP 设备应用


若要开始，请参阅分步 [构建 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)。

