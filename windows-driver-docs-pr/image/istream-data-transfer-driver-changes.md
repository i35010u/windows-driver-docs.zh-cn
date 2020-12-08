---
title: IStream 数据传输驱动程序更改
description: IStream 数据传输驱动程序更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f8a3f59615a55d2579620d9e3a7aa3a161d96b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808773"
---
# <a name="istream-data-transfer-driver-changes"></a>IStream 数据传输驱动程序更改


为了尽量减少对 Windows Vista 之前开发的驱动程序所做的更改，驱动程序无需实现任何新接口即可支持 **IStream** 数据传输。 而是通过 [IWiaMiniDrvCallBack 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)公开了一个新接口。 驱动程序可以为新的 **IWiaTransfer** 回调函数调用 **IWiaMiniDrvCallBack：： QueryInterface** ，这将向其提供对数据流和状态通知的访问权限。 Microsoft Windows SDK 文档中介绍了 **IWiaTransfer** 接口。

现在，驱动程序中的数据传输代码更简单，因为所有传输的处理方式都相同，没有文件或内存传输分支逻辑。

不支持 **IStream** 传输模型的驱动程序通常执行以下步骤：

1.  检查标志，确定请求是否用于上传或下载。

2.  获取 [IWiaMiniDrvCallBack](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback) 接口。

3.  从回调函数接收目标流。

4.  执行数据传输循环：
    1.  从设备接收数据。
    2.  将数据写入流。

但是，对于实现新的 **IStream** 传输模型的驱动程序，WIA 服务将不会调用 [**IWiaMiniDrv：:d rvwriteitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties) ，因为支持 *文件夹获取* 。

在文件夹获取中，单个传输请求位于父项上，但实际项属性位于正在传输的每个子项上。 不会为每个子项调用 **IWiaMiniDrv：:D rvwriteitemproperties** 方法，因此此方法不能用于对设备设置进行编程。 对于支持 **IStream** 数据传输的驱动程序，WIA 服务改为调用 [**IWiaMiniDrv：:d rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 。

**注意**  此更改仅影响支持新数据传输的驱动程序。 不支持 **IStream** 数据传输的旧驱动程序不受影响;WIA 服务将继续为它们调用 **IWiaMiniDrv：:D rvwriteitemproperties** 方法。

 

在文件夹获取中，驱动程序会对 **IWiaTransferCallback：： GetNextStream** (进行多次调用，) 在 Microsoft Windows SDK 文档中进行了介绍，该驱动程序一次只能有一个活动流。

驱动程序必须仅调用流的 **istream：： Write**、 **Istream：： Seek** 和 **IStream：： SetSize** 方法， (在下载操作期间 Windows SDK 文档) 中介绍了这些方法。 此限制使你可以更轻松地编写筛选器。 驱动程序不应预计目标流将实现任何其他方法。

当 " [**wia \_ DPS \_ 页面 \_ 大小**](./wia-dps-page-size.md) " 属性设置为 "wia 页面自动 (" 时，将 \_ 启用 " \_ 自动页面大小检测") ，驱动程序只应在完成图像数据传输后，为映像提供准确的维度信息。 对于基于流的传输，驱动程序应在传输结束时更新图像标头中的图像维度。 新会话开始时，"WIA \_ DPS \_ 页面大小" 属性的值 \_ 应始终设置为 "wia 页面自动" 以外的值 \_ \_ 。

 

