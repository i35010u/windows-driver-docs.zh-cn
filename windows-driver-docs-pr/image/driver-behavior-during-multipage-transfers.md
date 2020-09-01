---
title: 在多页传输过程中的驱动程序行为
description: 在多页传输过程中的驱动程序行为
ms.assetid: ecf0428b-c11c-49ff-9aa3-322e55dbca07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c53db9b4c0ecdba8536b5eed119afe9aa2dd45a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192509"
---
# <a name="driver-behavior-during-multipage-transfers"></a>在多页传输过程中的驱动程序行为


驱动程序无需直接支持文件夹获取。 如果驱动程序不支持，WIA 服务将以递归方式遍历项树，并对在[**WIA \_ IPA \_ 项 \_ FLAGS**](./wia-ipa-item-flags.md)属性中设置了**WiaItemTypeTransfer**位的所有项调用[**IWiaMiniDrv：:d rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 。

支持文件夹获取的驱动程序必须公开文件夹项的 " [**WIA \_ ip \_ 传输 \_ 功能**](./wia-ips-transfer-capabilities.md) " 属性。 此属性是一个标志属性，应 \_ 设置 WIA 传输 \_ 获取 \_ 子级功能， \_ 以指示它直接支持文件夹获取功能。 此支持意味着，驱动程序本身会遍历树以传输相关项，WIA 服务只会对文件夹调用 **IWiaMiniDrv：:D rvacquireitemdata** 。 驱动程序可以通过测试 WIA *lFlags* \_ 传输 \_ 获取子元素的 lFlags 参数来区分普通传输请求和文件夹获取请求 \_ 。

驱动程序支持直接获取文件夹的主要原因之一是效率。 与 WIA 服务对每个项调用传输相比，驱动程序可能会更有效地传输多个项。

这种情况的一个很好的例子就是多区域扫描。 当在扫描仪的平板上检测到多个区域 (如单独的图片) 时，它们可能会以儿童的形式表示。 下图显示了这种情况的一个示例。

![说明用于多区域扫描的项树的关系图](images/itemtree-multiregionscan.png)

如果在 "平台" 的每个子项上调用了单独的传输，则驱动程序将执行三次单独的扫描，这可能会非常耗时。 但是，如果在 "平台" 上请求了文件夹获取，则驱动程序将执行一次扫描，分解它并退回三个不同的区域 (这通常) 。

**注意**   建议仅将更复杂的驱动程序直接支持文件夹采集，因为驱动程序负责遍历项树并采取适当的措施。

 

 

