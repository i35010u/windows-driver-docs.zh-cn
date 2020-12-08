---
title: 微型驱动程序函数的调用顺序
description: 微型驱动程序函数的调用顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61b34ecb8f0ed62591dc8ee159a8d7e2098028c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804167"
---
# <a name="calling-order-for-minidriver-functions"></a>微型驱动程序函数的调用顺序





当微型驱动程序启动时，它将调用一些较旧的 STI 入口点，如 [**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)和 [**IStiUSD：： GetStatus**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)。 首个应用程序尝试与设备进行通信后，WIA 服务将调用 [**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)。 在此函数中，微型驱动程序应构造项树。

WIA 服务接下来会对树中的每个项调用 [**IWiaMiniDrv：:D rvinititemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties) 。 微型驱动程序应创建与该项相关的所有属性。 在某些情况下，可能需要创建一个空属性并在以后填写其数据。 例如，为了获得更好的性能，只应在 WIA 服务专门请求时才读取相机上的图像缩略图，如下所述。

要调用的下一个函数取决于应用程序和设备类型。 通常，应用程序的最常见操作是传输数据。 对于扫描仪，应用程序首先设置属性， (例如，数据类型和区) ，用于定义要从设备获取的映像。 当应用程序更改任何属性时，WIA 服务将调用 [**IWiaMiniDrv：:D rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 。 微型驱动程序应检查属性是否有效，如有必要，与设备进行通信。 通常，微型驱动程序应避免设置该函数中的属性，因为另一个应用程序可以在数据传输发生之前将属性设置为不同的值。

为了传输数据，WIA 服务会按顺序调用 [**IWiaMiniDrv：:D rvlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)、 [**IWiaMiniDrv：:d rvwriteitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)、 [**IWiaMiniDrv：:d Rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)和 [**IWiaMiniDrv：:d rvunlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)。 用于锁定和解锁设备的调用可确保在传输过程中没有其他应用程序访问设备。 对于扫描仪， **IWiaMiniDrv：:D rvwriteitemproperties** 应将属性（例如位置、范围和分辨率）发送到设备。 照相机驱动程序通常不需要将任何属性发送到设备。 **IWiaMiniDrv：:D rvacquireitemdata** 应该使用 [IWiaMiniDrvCallback COM 接口](iwiaminidrvcallback-com-interface.md)从设备检索图像数据，并通过 WIA 服务将其发送回应用程序。

对于照相机，如果应用程序想要显示图像的缩略图，WIA 服务会对每个图像调用 [**IWiaMiniDrv：:D rvreaditemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties) 。 微型驱动程序应在该点读取缩略图，并将其缓存在驱动程序项上下文中。 缓存缩略图非常重要，因为多个应用程序可能要求提供缩略图，导致多次调用 **IWiaMiniDrv：:D rvreaditemproperties**。 如果微型驱动程序在应用程序每次请求时读取缩略图，则性能会受到影响。

照相机的另一个特别注意事项是根项属性，它会影响照相机上的设置 (快门速度，例如) 。 当应用程序更改这些属性时，WIA 服务将调用 [**IWiaMiniDrv：:D rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)。 如有必要，微型驱动程序可以与照相机通信来验证属性设置。 但是，此函数不是更改相机上的设置的最佳位置，因为其他应用程序也可以更改属性。 调用 [**IWiaMiniDrv：:D rvdevicecommand**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand) 函数来捕获新映像时，微型驱动程序应从根项属性更新所有相机设置。

 

