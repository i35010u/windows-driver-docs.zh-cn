---
title: IStream 数据传输驱动程序更改
description: IStream 数据传输驱动程序更改
ms.assetid: 1c837e4f-8d53-40ed-8f5b-0d525c7dd758
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbcee2701620d01d965d8937fc1396573d57e895
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840805"
---
# <a name="istream-data-transfer-driver-changes"></a>IStream 数据传输驱动程序更改


为了尽量减少对 Windows Vista 之前开发的驱动程序所做的更改，驱动程序无需实现任何新接口即可支持**IStream**数据传输。 而是通过[IWiaMiniDrvCallBack 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)公开了一个新接口。 驱动程序可以为新的**IWiaTransfer**回调函数调用**IWiaMiniDrvCallBack：： QueryInterface** ，这将向其提供对数据流和状态通知的访问权限。 Microsoft Windows SDK 文档中介绍了**IWiaTransfer**接口。

现在，驱动程序中的数据传输代码更简单，因为所有传输的处理方式都相同，没有文件或内存传输分支逻辑。

不支持**IStream**传输模型的驱动程序通常执行以下步骤：

1.  检查标志，确定请求是否用于上传或下载。

2.  获取[IWiaMiniDrvCallBack](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)接口。

3.  从回调函数接收目标流。

4.  执行数据传输循环：
    1.  从设备接收数据。
    2.  将数据写入流。

但是，对于实现新的**IStream**传输模型的驱动程序，WIA 服务将不会调用[**IWiaMiniDrv：:d rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties) ，因为支持*文件夹获取*。

在文件夹获取中，单个传输请求位于父项上，但实际项属性位于正在传输的每个子项上。 不会为每个子项调用**IWiaMiniDrv：:D rvwriteitemproperties**方法，因此此方法不能用于对设备设置进行编程。 对于支持**IStream**数据传输的驱动程序，WIA 服务改为调用[**IWiaMiniDrv：:d rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 。

**请注意**  此更改仅影响支持新数据传输的驱动程序。 不支持**IStream**数据传输的旧驱动程序不受影响;WIA 服务将继续为它们调用**IWiaMiniDrv：:D rvwriteitemproperties**方法。

 

在文件夹收购中，驱动程序对**IWiaTransferCallback：： GetNextStream** （在 Microsoft Windows SDK 文档中进行了介绍）的多次调用，该驱动程序一次只能有一个活动流。

在下载操作过程中，驱动程序必须仅调用流的**istream：： Write**、 **Istream：： Seek**和**IStream：： SetSize**方法（在 Windows SDK 文档中进行了介绍）。 此限制使你可以更轻松地编写筛选器。 驱动程序不应预计目标流将实现任何其他方法。

当[**wia\_DPS\_页\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)属性设置为 WIA\_页面\_自动（即启用了自动页面大小检测）时，驱动程序应提供有关映像的准确维度信息完成图像数据的传输。 对于基于流的传输，驱动程序应在传输结束时更新图像标头中的图像维度。 在新会话开始时，WIA\_DPS\_页\_大小属性的值应始终设置为 WIA\_页面\_自动值。

 

 




