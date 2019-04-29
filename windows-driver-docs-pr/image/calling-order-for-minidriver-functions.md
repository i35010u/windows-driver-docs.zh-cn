---
title: 微型驱动程序函数的调用顺序
description: 微型驱动程序函数的调用顺序
ms.assetid: 0e51d29c-964d-44d5-86be-095601286f94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31bd38f8d3139dc32cf1b2c7b8f4adceed7e968b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373353"
---
# <a name="calling-order-for-minidriver-functions"></a>微型驱动程序函数的调用顺序





微型驱动程序启动时，它将调用一些较旧的 STI 入口点，如[ **IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824)，并[ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823). 只要第一个应用程序尝试与设备通信，WIA 的服务调用[ **IWiaMiniDrv::drvInitializeWia**](https://msdn.microsoft.com/library/windows/hardware/ff544986)。 它在此函数是，微型驱动程序应构造项树。

WIA 服务下一步调用[ **IWiaMiniDrv::drvInitItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff544989)在树中每个项。 微型驱动程序应创建与该项相关的所有属性。 在某些情况下，可能会创建一个空属性和更高版本在其数据填充明智之举。 例如，为了提高性能，相机上的图像缩略图应读取在仅当 WIA 服务专门请求，如下所述。

若要调用的下一步函数取决于应用程序和设备类型。 通常情况下，应用程序的最常见的操作将数据传输。 对于扫描程序，该应用程序首先会设置定义它想要从设备获取的映像的属性 （例如，数据类型和范围）。 WIA 服务调用[ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)应用程序时更改任何属性。 微型驱动程序应检查属性有效，如有必要与设备通信。 微型驱动程序通常应避免在该函数中，设置属性，因为数据传输发生之前另一个应用程序无法将属性设置为不同的值。

若要传输的数据，WIA 服务调用[ **IWiaMiniDrv::drvLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544995)， [ **IWiaMiniDrv::drvWriteItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545020)， [**IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)，和[ **IWiaMiniDrv::drvUnLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff545012)按顺序。 用于锁定和解锁该设备的调用保证其他应用程序未在传输期间访问设备。 有关扫描仪**IWiaMiniDrv::drvWriteItemProperties**应发送到设备的属性，如位置、 范围和解决方法。 照相机的驱动程序通常不需要向设备发送的任何属性。 **IWiaMiniDrv::drvAcquireItemData**应从设备中检索图像数据并将其发送回应用程序通过 WIA 服务中，使用[IWiaMiniDrvCallback COM 接口](iwiaminidrvcallback-com-interface.md)。

对于相机，如果应用程序想要显示图像的缩略图 WIA 服务调用[ **IWiaMiniDrv::drvReadItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545005)上每个映像。 微型驱动程序应在该点读取缩略图，其缓存中的驱动程序项上下文。 务必要缓存该缩略图，因为多个应用程序可能会要求为缩略图，从而导致多次调用**IWiaMiniDrv::drvReadItemProperties**。 如果微型驱动程序读取每次应用程序请求的缩略图，性能将受到影响。

用于相机的一个其他特殊注意事项是影响照相机 （例如快门速度） 上的设置的根项属性。 当应用程序更改这些属性时，WIA 服务调用[ **IWiaMiniDrv::drvValidateItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545017)。 如有必要，若要验证的属性设置，微型驱动程序可以使用照相机，进行通信。 此函数，但是，不更改摄像机上的设置的最佳位置因为另一个应用程序还可以更改的属性。 微型驱动程序应更新的所有相机设置从根项属性时[ **IWiaMiniDrv::drvDeviceCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff543967)函数调用以捕获新映像。

 

 




