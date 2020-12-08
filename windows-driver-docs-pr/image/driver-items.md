---
title: 驱动程序项
description: 驱动程序项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ded530745b588e1676810e2009a22861d195c20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818989"
---
# <a name="driver-items"></a>驱动程序项





属性存储在 WIA 驱动程序项中。 驱动程序项是对静止图像设备以及设备存储或生成的数据的逻辑描述。 WIA 微型驱动程序使用 WIA 服务库中的函数创建 WIA 驱动程序项。

WIA 驱动程序通常包含多个驱动程序项。 第一个驱动程序项是必需的，它是静态图像设备的逻辑表示形式，称为 *根项*。 根项包含一些属性，这些属性描述物理静止图像设备的特性和设置。

下图是根项的示例。

![阐释 wia 驱动程序根项的关系图](images/wia-rootdriveritem.png)

静止图像设备还必须描述设备存储或生成的数据。 例如，照相机可以在其媒体上存储多个图像 (或其他媒体格式) 。 每个映像都可以有信息，如唯一名称和图像尺寸。 WIA 微型驱动程序模型允许驱动程序将信息存储在 *子项* 中。 子项包含描述它所表示的数据特征的属性。

下图显示了子项的示例。

![说明 wia 驱动程序子项的关系图](images/wia-childdriveritem.png)

与在包含目录和文件的新式文件系统中找到的目录层次结构类似，WIA 微型驱动程序模型将根和子项存储在称为 *项树* 的层次结构中。 WIA 微型驱动程序使用 WIA 服务库来创建对设备及其数据进行逻辑描述的根和子驱动程序项。 对于数字照相机设备或存储多个图像的任何静止图像设备，项树类似于具有一个根项和多个子项的目录结构。

下图是微型驱动程序为数字照相机创建的项树的示例。

![阐释 wia 驱动程序项树的关系图](images/wia-rootdriveritem3.png)

对于简单的平板扫描仪设备，或者没有存储的任何静止图像设备，项树仅包含一个子项目。 建议以专门标识设备的方式命名子项。 例如，平板扫描仪从扫描仪平台获取其数据;因此，子项目应命名为 "平台"。

下图说明了微型驱动程序为简单平板扫描仪创建的项树。

![阐释 wia 驱动程序平板项目树的示意图](images/wia-rootdriveritem2.png)

有关驱动程序项的详细信息，请参阅 [开发 Wia 驱动程序：基本概念](developing-a-wia-driver--basic-concepts.md)、 [开发 Wia 扫描器驱动程序](developing-a-wia-scanner-driver.md) 和 [开发 wia 相机驱动程序](developing-a-wia-camera-driver.md)。

 

 




