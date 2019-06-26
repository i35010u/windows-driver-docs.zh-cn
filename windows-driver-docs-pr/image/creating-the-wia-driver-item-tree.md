---
title: 创建 WIA 驱动程序项树
description: 创建 WIA 驱动程序项树
ms.assetid: 3ae489b9-175e-4b1e-a6c8-a72a3a3c212a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127a4002016604ba29c997c2535e9c6231809713
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370071"
---
# <a name="creating-the-wia-driver-item-tree"></a>创建 WIA 驱动程序项树





初始化微型驱动程序后，它必须创建中的驱动程序项树[ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法：

1.  如果尚不存在，请创建驱动程序项树。 微型驱动程序设置的根项标志，通过调用驱动程序服务库函数创建根项[ **wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)。 微型驱动程序将返回的指针到根项存储在私有成员变量中。

2.  设备使用的每个项的项创建子[ **wiasCreateDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)函数。 此函数创建微型驱动程序可以在其中存储有关项目的信息特定于设备的上下文。

3.  调用[ **IWiaDrvItem::AddItemToFolder** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)上每个子项，若要将项添加到驱动程序项树的方法。

 

 




