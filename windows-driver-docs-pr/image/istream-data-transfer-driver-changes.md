---
title: IStream 数据传输驱动程序更改
description: IStream 数据传输驱动程序更改
ms.assetid: 1c837e4f-8d53-40ed-8f5b-0d525c7dd758
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30c7658c9251d613b86f742639f2bd4a99569f03
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378883"
---
# <a name="istream-data-transfer-driver-changes"></a>IStream 数据传输驱动程序更改


为了尽量减少对 Windows Vista 之前开发的驱动程序的更改，驱动程序无需实现任何新接口以支持**IStream**数据传输。 相反，通过公开新的接口已[IWiaMiniDrvCallBack 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)。 驱动程序可以调用**IWiaMiniDrvCallBack::QueryInterface**新**IWiaTransfer**回调函数，将使他们能够访问的数据的流和状态通知。 **IWiaTransfer** Microsoft Windows SDK 文档中详细介绍了接口。

驱动程序内的数据传输代码现更简单，因为所有传输都处理相同的方式，使用任何文件或内存传输分支逻辑。

不支持的驱动程序**IStream**传输模型通常执行以下步骤：

1.  检查以确定请求是否上传或下载的标志。

2.  获取[IWiaMiniDrvCallBack](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)接口。

3.  从回调函数接收的目标流。

4.  执行数据传输循环：
    1.  从设备接收数据。
    2.  向流写入数据。

但是，对于实现新的驱动程序**IStream**传输模型，将不会调用 WIA 服务[ **IWiaMiniDrv::drvWriteItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)因为*文件夹获取*支持。

在文件夹获取单个传输请求是在父项中，但实际项属性是在每个要传输的子项。 **IWiaMiniDrv::drvWriteItemProperties**不会调用方法的每个子项，因此无法使用此方法进行编程的设备设置。 有关支持的驱动程序**IStream** WIA 服务调用的数据传输[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)相反。

**请注意**  此更改会影响仅支持将新的数据传输的驱动程序。 旧驱动程序，它不支持**IStream**数据传输，不会受到影响; WIA 服务将继续调用**IWiaMiniDrv::drvWriteItemProperties**为它们的方法。

 

在驱动程序，其中可以对多个调用文件夹收购**IWiaTransferCallback::GetNextStream** （这介绍 Microsoft Windows SDK 文档中），该驱动程序可以有一次只有一个活动流。

该驱动程序必须调用仅此流的**IStream::Write**， **IStream::Seek**，并**IStream::SetSize**方法 （这 Windows SDK 文档中所述）在下载操作。 此限制，使你更轻松地编写筛选器。 该驱动程序不应期望目标流将实现的任何其他方法。

当[ **WIA\_DPS\_页\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)属性设置为 WIA\_页\_自动 （即，自动页大小检测是已启用），该驱动程序应提供有关映像的准确维度信息仅后完成的图像数据传输。 对于基于流的传输模式，该驱动程序应更新映像标头传输结束时将图像尺寸。 在新的会话，WIA 的值开头\_DPS\_页面\_SIZE 属性应始终设置为 WIA 以外的值\_页\_自动。

 

 




