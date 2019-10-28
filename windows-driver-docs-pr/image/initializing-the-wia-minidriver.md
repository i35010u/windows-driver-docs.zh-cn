---
title: 初始化 WIA 微型驱动程序
description: 初始化 WIA 微型驱动程序
ms.assetid: 9ccb136b-41f7-438a-9e07-1fd7c8971417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3920242e4c98a4e7067e53376c1c237b6fea95e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840819"
---
# <a name="initializing-the-wia-minidriver"></a>初始化 WIA 微型驱动程序





实现[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)的第一步是初始化微型驱动程序，并创建驱动程序项的层次结构树。 为此，WIA 服务会在客户端应用程序每次尝试使用设备时调用[**IWiaMiniDrv：:D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法。 如果两个或多个应用程序同时使用设备，WIA 服务将为每个应用程序调用此方法。 在此方法中，微型驱动程序通常会执行以下操作：

1.  初始化从 WIA 服务传入的参数。

2.  保存 PStiDevice 指向的 STI 设备接口 *。* 完成此操作后，可以使用[**IStiDevice：： LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice)和[**IStiDevice：： UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice)方法锁定或解锁 WIA 设备。

3.  将*bstrDeviceID*和*bstrRootFullItemName*缓存在成员变量中，以便其他方法可以使用这些变量。

4.  打开设备的句柄。 （建议将此步骤用于非共享端口，如 USB、SCSI 和1394。）

5.  生成项树，如[创建 WIA 驱动程序项树](creating-the-wia-driver-item-tree.md)中所述。

**IWiaMiniDrv：:D rvinitializewia**方法还可用于创建和初始化驱动程序使用的动态数组和结构。 例如，可以创建驱动程序支持的命令和事件的数组，供[**IWiaMiniDrv：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法以后使用。

**请注意**   在调用**IWiaMiniDrv：:D rvinitializewia**之前，可以调用[**IWiaMiniDrv：:d rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法。 当 WIA 服务需要在应用程序使用设备之前查询事件信息时，可能会发生这种情况。 仅当应用程序发出信号来使用设备时，才会调用**IWiaMiniDrv：:D rvinitializewia**方法。

 

### <a name="keeping-track-of-application-connections"></a>跟踪应用程序连接

如前所述，当应用程序要与 WIA 设备通信时，WIA 服务将调用相应的驱动程序的[**IWiaMiniDrv：:D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法。 当应用程序完成设备并释放对它的所有 WIA 引用时，WIA 服务将调用相应的驱动程序的[**IWiaMiniDrv：:D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)方法。 请注意，WIA 支持多个同时进行的应用程序连接。 这意味着两个或更多应用程序可以请求与同一设备相关联的 WIA 接口。 但这并不意味着，驱动程序必须处理同时进行的请求;WIA 服务确保一次只向驱动程序发送一个请求。 但是，WIA 服务在调用**IWiaMiniDrv：:D rvuninitializewia**方法之前，可以多次调用**IWiaMiniDrv：:d rvinitializewia**方法。

此信息为什么有用？ 通常，当应用程序使用驱动程序时，可能需要使用这些资源，如 WIA 驱动程序项树、图像筛选库等。 由于这些资源可能占用大量内存，因此最好在不需要时将其卸载。

**请注意**   **IWiaMiniDrv：:D rvinitializewia**和**IWiaMiniDrv：:d rvuninitializewia**方法仅用于通知应用程序连接的驱动程序。 WIA 服务可以调用其他驱动程序方法，而无需先调用**IWiaMiniDrv：:D rvinitializewia**，这意味着 WIA 服务不一定在完成后调用**IWiaMiniDrv：:d rvuninitializewia** 。 调用的方法是不需要 WIA 项的信息性方法，例如[**IWiaMiniDrv：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)和[**IWiaMiniDrv：:d rvgetwiaformatinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)。

 

本部分包含以下主题：

[调用微型驱动程序函数的顺序](calling-order-for-minidriver-functions.md)

[加载和卸载 WIA 微型驱动程序](loading-and-unloading-a-wia-minidriver.md)

[连接和断开 WIA 应用程序](connecting-and-disconnecting-a-wia-application.md)

[报告 WIA 微型驱动程序状态](reporting-wia-minidriver-status.md)

 

 




