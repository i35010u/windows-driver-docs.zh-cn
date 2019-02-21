---
title: 创建 WIA 驱动程序项树
description: 创建 WIA 驱动程序项树
ms.assetid: 3ae489b9-175e-4b1e-a6c8-a72a3a3c212a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4077776f9abfd7925172feca885ae5e6a35a2bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524538"
---
# <a name="creating-the-wia-driver-item-tree"></a>创建 WIA 驱动程序项树





初始化微型驱动程序后，它必须创建中的驱动程序项树[ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)方法：

1.  如果尚不存在，请创建驱动程序项树。 微型驱动程序设置的根项标志，通过调用驱动程序服务库函数创建根项[ **wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)。 微型驱动程序将返回的指针到根项存储在私有成员变量中。

2.  设备使用的每个项的项创建子[ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)函数。 此函数创建微型驱动程序可以在其中存储有关项目的信息特定于设备的上下文。

3.  调用[ **IWiaDrvItem::AddItemToFolder** ](https://msdn.microsoft.com/library/windows/hardware/ff543856)上每个子项，若要将项添加到驱动程序项树的方法。

 

 




