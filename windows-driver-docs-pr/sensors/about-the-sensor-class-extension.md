---
title: 有关传感器类扩展
description: 有关传感器类扩展
ms.assetid: 4b55e5fe-2947-4511-ba2d-479d5fd83ebe
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4b54940ff286a4c5bc794bd16f948a59ae128a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547105"
---
# <a name="about-the-sensor-class-extension"></a>有关传感器类扩展


若要更加轻松地编写公开传感器到 Windows （和特别的传感器和位置平台），Windows 的设备驱动程序包括一个传感器驱动程序类扩展， [ISensorClassExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nn-sensorsclassextension-isensorclassextension)接口。 传感器设备驱动程序的必需的组件，该 COM 对象提供一组简单的接口，使程序员可以实施传感器驱动程序，而编写大量的样板代码。 此外，此类扩展提供以下优势：

-   有助于确保用户隐私良好保护，因为此类扩展会强制执行相应控件的访问限制处理个人信息的传感器。

-   提供从驱动程序检索数据，并将引发事件通知的 API 层通过一个标准方式。

 

 




