---
title: 创建 WIA 照相机项树布局
description: 创建 WIA 照相机项树布局
ms.assetid: 83b496dc-8c47-46fb-b703-837eb536cb66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11bf5496941d34ac84e1c2bca748e7cca915d184
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370962"
---
# <a name="creating-a-wia-camera-item-tree-layout"></a>创建 WIA 照相机项树布局





Microsoft Windows Me 和 Windows XP 的 WIA 照相机项树包含根项，并表示映像和存储在照相机设备上的文件夹的子项目。 请参阅[初始化 WIA 微型驱动程序](initializing-the-wia-minidriver.md)获取有关如何创建一个项树的示例。 下图显示了 Windows Me 和 Windows XP 项树。

![说明 wia 照相机项的关系图树适用于 windows me 和 windows xp](images/camera-tree.png)

在 Windows Vista 和更高版本操作系统中的照相机树关系图，请参阅[WIA 项标志的示例使用情况和类别](example-usage-of-wia-item-flags-and-categories.md)。

照相机项树的根项目包含所有标准 WIA 微型驱动程序信息和特定于照相机的属性。 特定于照相机的属性包括拍摄图片数和其他照相机控件的属性。

照相机项树的子项目表示的图像或存储在设备上的文件夹。 建议微型驱动程序消除任何不必要的文件夹，以允许更轻松地访问转让项级别。 这使访问 WIA 项由应用程序更容易，并阻止用户无需深入了解以获取到实际的图像的文件夹结构导航。

微型驱动程序编写器可以使文件和文件夹项任何命名他或她的需求。 但是，WIA 项树中的每一项表示摄像机上的物理数据项，并且应提供建议摄像机中的实际数据项目的名称。

时添加到或从照相机中删除了数据项，它负责的 WIA 微型驱动程序与相机的内容同步其 WIA 项树。 有关如何完成此操作的示例，请参阅[更改 WIA 项树结构](changing-the-wia-item-tree-structure.md)。

通过 WIA 的服务，应用程序可以执行以下操作：

-   查询照相机功能。

-   设置相机的设备属性。

-   请求数据传输。

 

 




