---
title: 初始化 WIA 微型驱动程序
description: 初始化 WIA 微型驱动程序
ms.assetid: 9ccb136b-41f7-438a-9e07-1fd7c8971417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af688c22e8e686bd1362a440e9fe315776ca96a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378942"
---
# <a name="initializing-the-wia-minidriver"></a>初始化 WIA 微型驱动程序





实现的第一步[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)是初始化微型驱动程序并创建驱动程序的项的层次结构树。 若要执行此操作，WIA 服务调用[ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法每次客户端应用程序想要使用的设备。 如果两个或多个应用程序同时使用的设备，WIA 服务每个应用程序调用此方法。 在此方法，微型驱动程序通常执行以下操作：

1.  初始化 WIA 服务从传入的参数。

2.  保存指向 STI 设备接口*pStiDevice。* 这是，以便[ **IStiDevice::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice)并[ **IStiDevice::UnLockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice)方法可用于锁定或解锁 WIA设备。

3.  缓存*bstrDeviceID*并*bstrRootFullItemName*在成员变量，以便它们可由其他方法。

4.  将打开到设备的句柄。 （此步骤被推荐用于非共享端口，例如 USB、 SCSI、 和 1394年。）

5.  生成项树中，如中所述[创建 WIA 驱动程序项树](creating-the-wia-driver-item-tree.md)。

**IWiaMiniDrv::drvInitializeWia**方法还可用于创建和初始化的动态数组和驱动程序使用的结构。 例如，命令和事件驱动程序支持可为更高版本使用创建的数组[ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法。

**请注意**   [ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)可能之前调用方法**IWiaMiniDrv::drvInitializeWia**调用。 这可以 WIA 服务需要的应用程序存在使用该设备之前查询事件的信息。 **IWiaMiniDrv::drvInitializeWia**仅当应用程序向其意图来使用该设备发出信号时调用方法。

 

### <a name="keeping-track-of-application-connections"></a>跟踪的应用程序连接

如前所述，应用程序意图与 WIA 设备进行通信时，WIA 服务会调用相应的驱动程序[ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法。 当应用程序与设备完成并释放所有 WIA 引用时，WIA 服务调用相应的驱动程序[ **IWiaMiniDrv::drvUnInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)方法。 请注意，WIA 支持多个同时进行的应用程序连接。 这意味着两个或多个应用程序可以请求与在同一设备相关联的 WIA 接口。 它并不意味着，不过，该驱动程序必须处理并发请求数;WIA 服务可确保一次只有一个请求发送到该驱动程序。 但是，可以调用 WIA 服务**IWiaMiniDrv::drvInitializeWia**方法调用之前多次**IWiaMiniDrv::drvUnInitializeWia**方法。

为什么此信息很有用？ 通常是驱动程序时应用程序在使用它们，如 WIA 驱动程序项树、 的图像筛选库，以及其他可能需要的资源。 因为这些资源会占用大量内存，最好将它们卸载时不需要它们。

**请注意**   **IWiaMiniDrv::drvInitializeWia**并**IWiaMiniDrv::drvUnInitializeWia**方法用于通知的仅限应用程序连接的驱动程序。 WIA 服务可以调用其他驱动程序的方法没有首先调用**IWiaMiniDrv::drvInitializeWia**，这意味着，WIA 服务不一定需要**IWiaMiniDrv::drvUnInitializeWia**完成时。 调用的方法是信息性方法，如不需要 WIA 项[ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)并[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo).

 

本部分包含以下主题：

[调用微型驱动程序函数顺序](calling-order-for-minidriver-functions.md)

[加载和卸载 WIA 微型驱动程序](loading-and-unloading-a-wia-minidriver.md)

[连接和断开 WIA 应用程序](connecting-and-disconnecting-a-wia-application.md)

[报告 WIA 微型驱动程序状态](reporting-wia-minidriver-status.md)

 

 




