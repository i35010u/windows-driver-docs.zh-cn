---
title: 在多页传输过程中的驱动程序行为
description: 在多页传输过程中的驱动程序行为
ms.assetid: ecf0428b-c11c-49ff-9aa3-322e55dbca07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75806e0c93f4b7236db5d0d9124f7cad33fb7551
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840852"
---
# <a name="driver-behavior-during-multipage-transfers"></a>在多页传输过程中的驱动程序行为


驱动程序无需直接支持文件夹获取。 如果驱动程序不支持驱动程序，WIA 服务将以递归方式遍历项树，并对在[**WIA\_IPA\_项**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)中设置**WiaItemTypeTransfer**位的所有项调用[**IWIAMINIDRV：:d rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)\_标志知识产权.

支持文件夹获取的驱动程序必须向文件夹项公开[**WIA\_ip\_传输\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-transfer-capabilities)属性。 此属性是一个标志属性，应将 WIA\_传输\_获取\_\_子级，以指示它直接支持文件夹获取功能。 此支持意味着，驱动程序本身会遍历树以传输相关项，WIA 服务只会对文件夹调用**IWiaMiniDrv：:D rvacquireitemdata** 。 驱动程序可以通过测试 WIA\_传输的*lFlags*参数\_获取\_子位，来区分普通传输请求和文件夹获取请求。

驱动程序支持直接获取文件夹的主要原因之一是效率。 与 WIA 服务对每个项调用传输相比，驱动程序可能会更有效地传输多个项。

这种情况的一个很好的例子就是多区域扫描。 当在扫描仪的平板上检测到多个区域（如单独的图片）时，它们可以表示为 "平板" 项目外的子项。 下图显示了这种情况的一个示例。

![说明用于多区域扫描的项树的关系图](images/itemtree-multiregionscan.png)

如果在 "平台" 的每个子项上调用了单独的传输，则驱动程序将执行三次单独的扫描，这可能会非常耗时。 但是，如果在 "平台" 上请求了文件夹购置，驱动程序将执行一次扫描，分解它，然后手动装回三个不同的区域（这通常更快）。

**请注意**  建议仅将更复杂的驱动程序直接支持文件夹采集，因为驱动程序负责遍历项树并采取适当的措施。

 

 

 




