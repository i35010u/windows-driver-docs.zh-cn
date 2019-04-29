---
title: 驱动程序项
description: 驱动程序项
ms.assetid: 7b557c92-400e-45e5-bee6-328489d20cae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c76041ecda460b7954b83fa91a9f94e26a09275
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364507"
---
# <a name="driver-items"></a>驱动程序项





属性存储在 WIA 驱动程序项目中。 驱动程序项是静态的图像设备和设备存储或生成的数据的逻辑说明。 WIA 微型驱动程序创建一个 WIA 驱动程序项，通过使用 WIA 的服务库中的功能。

WIA 驱动程序通常具有多个驱动程序项目。 第一个驱动程序项目，这是必需的进行静态图像设备的逻辑表示形式，并调用*根项*。 根项目包含特征进行了说明这些属性和设置的物理静止图像的设备。

下图是根项的示例。

![说明 wia 驱动程序的根项的关系图](images/wia-rootdriveritem.png)

静态图像设备还必须描述设备存储或生成的数据。 例如，照相机可以存储多个映像 （或其他媒体格式） 上其媒体。 每个映像可以有一个唯一的名称和图像的尺寸等信息。 WIA 微型驱动程序模型允许驱动程序存储中的信息*子项*。 子项目包含描述它所代表的数据的特征的属性。

下图显示了子项目的示例。

![说明 wia 驱动程序子项目的关系图](images/wia-childdriveritem.png)

与目录和文件组成的现代文件系统中找到的目录层次结构类似，WIA 微型驱动程序模型存储根和子项目是层次结构中称为*项树*。 WIA 微型驱动程序使用 WIA 服务库来创建根和子逻辑上描述的设备和其数据的驱动程序项目。 对于数字照相机的设备或将多个映像存储任何静态图像设备，项树类似于具有一个根项目和许多子项目的目录结构。

下图是为数码照相机的微型驱动程序创建一个项树的示例。

![说明 wia 驱动程序项树的关系图](images/wia-rootdriveritem3.png)

对于简单平板扫描仪设备或没有存储任何静态图像设备，项树包含只有一个子项目。 我们建议专门标识的设备的方式，命名为子项目。 例如，平板扫描仪获取来自扫描仪平台; 其数据因此，子项目应命名为"平板。"

下图说明了为简单平板扫描仪的微型驱动程序创建一个项树。

![说明 wia 驱动程序平板项树的关系图](images/wia-rootdriveritem2.png)

有关驱动程序项目的详细信息，请参阅[开发 WIA 驱动程序：基本概念](developing-a-wia-driver--basic-concepts.md)，[开发 WIA 扫描程序驱动程序](developing-a-wia-scanner-driver.md)并[开发 WIA 照相机驱动程序](developing-a-wia-camera-driver.md)。

 

 




