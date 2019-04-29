---
title: 在多页传输过程中的驱动程序行为
description: 在多页传输过程中的驱动程序行为
ms.assetid: ecf0428b-c11c-49ff-9aa3-322e55dbca07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c5d0fd08773bbf980c24bbc4469fc622cf746ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364514"
---
# <a name="driver-behavior-during-multipage-transfers"></a>在多页传输过程中的驱动程序行为


驱动程序无需直接支持文件夹获取。 如果驱动程序不支持它，WIA 服务将以递归方式遍历项树并调用[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)上的所有项目**WiaItemTypeTransfer**中设置位[ **WIA\_IPA\_项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff551585)属性。

直接支持文件夹获取的驱动程序必须公开[ **WIA\_IPS\_传输\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff552657)文件夹项的属性。 此属性是一个标记属性，因此应具有 WIA\_传输\_ACQUIRE\_子级\_能够位集以指示它直接支持文件夹获取功能。 此支持意味着驱动程序本身将遍历树要传输的相关项和 WIA 服务将只需调用**IWiaMiniDrv::drvAcquireItemData**文件夹上。 该驱动程序可以通过测试来区分之间正常传输请求和文件夹获取请求*lFlags* WIA 的参数\_传输\_ACQUIRE\_子级位。

驱动程序，将直接支持文件夹获取的主要原因之一是效率。 驱动程序可能会传输比具有对每个项调用传输 WIA 服务更加有效地在多个项。

这种情况下的一个很好示例是在多区域的扫描过程。 在扫描程序的平台检测到多个区域 （如单独的图片） 后，它们可以表示为关闭的"平台"项的子级。 下图中表示这种情况的示例。

![说明用于多区域扫描项树的关系图](images/itemtree-multiregionscan.png)

如果单独传输上的"平台"的子项的每个调用，该驱动程序会执行三个单独的扫描，可能需要较长时间。 但是，如果文件夹获取已请求在"平台"，该驱动程序将执行一次扫描、 分解它，然后退回三个不同的区域 （这是通常更快）。

**请注意**  我们建议仅更复杂的驱动程序直接支持文件夹获取，因为该驱动程序负责项树的每个步骤并采取适当措施。

 

 

 




