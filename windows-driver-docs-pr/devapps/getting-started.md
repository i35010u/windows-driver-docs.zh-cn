---
title: 开始使用 UWP 设备应用程序
description: 从这里开始构建 UWP 设备应用。
ms.assetid: 6280E9CC-422B-4100-8B38-07BADD6A578A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4189c4b4978a106f21e8197889cb4107a7b3e75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387959"
---
# <a name="getting-started-with-uwp-device-apps"></a>开始使用 UWP 设备应用程序


从这里开始构建 UWP 设备应用。

![开始使用 windows 应用商店设备应用程序](images/devices-diagram-350x350.png)

设备制造商可以创建用作设备配套的 UWP 设备应用。 UWP 设备应用的功能超出常规的 UWP 应用，可执行特权操作，例如固件更新。 此外，UWP 设备应用程序可以从自动播放开始 （在多个设备不是其他应用程序也能）、 自动安装第一次设备连接，和扩展内置于 Windows 的打印机和相机体验。

**请注意**  Windows 运行时设备 Api 不需要的设备元数据。 这意味着您的应用程序不必是一个 UWP 设备应用来使用它们。 UWP 应用可以使用这些 Api 来访问 USB、 人体学接口设备 (HID)、 蓝牙设备和的详细信息。 有关详细信息，请参阅[集成设备](https://go.microsoft.com/fwlink/p/?LinkId=533279)。

 

若要了解 UWP 移动宽带应用，请参阅 [Mobile Broadband](https://go.microsoft.com/fwlink/p/?LinkID=301754)（移动宽带）。

## <a name="span-id1getsetupspanspan-id1getsetupspan1-get-set-up"></a><span id="1._get_set_up"></span><span id="1._GET_SET_UP"></span>1.准备工作


若要开发 UWP 设备应用： 需要 Microsoft Visual Studio 中，为开发 UWP 应用和设备元数据创建向导，为开发设备元数据。

**请注意**  开发 UWP 应用在 Windows 10 的设备应用程序，下载 Microsoft Visual Studio 2017 和 Windows Driver Kit (WDK) 10。 [成为 Windows 预览体验获取工具包和工具](https://go.microsoft.com/fwlink/p/?LinkId=526775)

 

### <a name="span-idifyourealsodevelopingdriversspanspan-idifyourealsodevelopingdriversspanspan-idifyourealsodevelopingdriversspanif-youre-also-developing-drivers"></a><span id="If_you_re_also_developing_drivers"></span><span id="if_you_re_also_developing_drivers"></span><span id="IF_YOU_RE_ALSO_DEVELOPING_DRIVERS"></span>如果您还开发驱动程序

如果要开发除 UWP 设备应用程序的 Windows 驱动程序，使用 Microsoft Visual Studio Professional 或 Microsoft Visual Studio Ultimate 创建 UWP 设备应用程序。 这些版本包括新的设备元数据创建向导和，也需要通过 Windows Driver Kit (WDK) 8.1。

1.  [下载 Visual Studio 专业版或 Visual Studio 旗舰版](https://go.microsoft.com/fwlink/p/?LinkId=302196)
2.  [下载 WDK 8.1](https://go.microsoft.com/fwlink/p/?LinkId=302196)

### <a name="span-idifyourenotgoingtobedevelopingdriversspanspan-idifyourenotgoingtobedevelopingdriversspanspan-idifyourenotgoingtobedevelopingdriversspanif-youre-not-going-to-be-developing-drivers"></a><span id="If_you_re_not_going_to_be_developing_drivers"></span><span id="if_you_re_not_going_to_be_developing_drivers"></span><span id="IF_YOU_RE_NOT_GOING_TO_BE_DEVELOPING_DRIVERS"></span>如果您不打算开发驱动程序

如果您不需要开发驱动程序，可以使用 Microsoft Visual Studio Express 2015 for Windows 创建 UWP 设备应用程序。 但此版本的 Visual Studio 安装不包括设备元数据创建向导的 sdk 版本。 若要获取新的设备元数据创建向导，还必须下载独立 Windows 8.1 SDK。

1.  [下载 Visual Studio Express 2015 for Windows 10](https://visualstudio.microsoft.com/vs/express/)
2.  [下载独立 Windows 8.1 SDK](https://go.microsoft.com/fwlink/p/?LinkId=302196)

## <a name="span-id2buildsomeregularwindowsstoreappsspanspan-id2buildsomeregularwindowsstoreappsspan2-build-some-regular-uwp-apps"></a><span id="2._build_some_regular_windows_store_apps"></span><span id="2._BUILD_SOME_REGULAR_WINDOWS_STORE_APPS"></span>2.生成一些常规的 UWP 应用


UWP 设备应用程序是一种特殊的 UWP 应用。 因此，开发第一个 UWP 设备应用程序之前，完成设置以生成一些常规的 UWP 应用。

-   [注册-Microsoft Store 开发人员帐户注册](https://go.microsoft.com/fwlink/p/?LinkId=302197)
-   [开始使用 Microsoft Visual Studio](https://go.microsoft.com/fwlink/p/?LinkID=267230)
-   请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)

## <a name="span-id3learnwhatmakeswindowsstoredeviceappsspecialspanspan-id3learnwhatmakeswindowsstoredeviceappsspecialspan3-learn-what-makes-uwp-device-apps-special"></a><span id="3._learn_what_makes_windows_store_device_apps_special"></span><span id="3._LEARN_WHAT_MAKES_WINDOWS_STORE_DEVICE_APPS_SPECIAL"></span>3.了解是什么使 UWP 设备应用特殊


了解如何使用 UWP 设备应用和所需构建一个特殊内容。

-   [满足 UWP 设备应用程序](meet-uwp-device-apps.md)
-   [构建 UWP 设备应用程序](the-workflow.md)

## <a name="span-id4downloadsamplesspanspan-id4downloadsamplesspan4-download-samples"></a><span id="4._download_samples"></span><span id="4._DOWNLOAD_SAMPLES"></span>4.下载示例


你可以找到与设备相关示例[设备和传感器](https://go.microsoft.com/fwlink/p/?LinkID=302213)示例库中的关键字。 了解如何在完整示例的上下文中使用 Api。 您可以告知 UWP 设备应用，因为它包含一个 StoreManifest.xml 文件，将其与设备元数据关联。 这些示例都标记有[UWP 设备应用](https://go.microsoft.com/fwlink/p/?LinkID=299847)关键字。

## <a name="span-id4buildyourownwindowsstoredeviceappspanspan-id4buildyourownwindowsstoredeviceappspan4-build-your-own-uwp-device-app"></a><span id="4._build_your_own_windows_store_device_app"></span><span id="4._BUILD_YOUR_OWN_WINDOWS_STORE_DEVICE_APP"></span>4.构建 UWP 设备应用


若要开始，请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)。

 

 





