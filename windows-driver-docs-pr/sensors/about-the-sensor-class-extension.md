---
title: 关于传感器类扩展
description: 关于传感器类扩展
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f6c705a928dee177b13a064556482d1263cf186d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831089"
---
# <a name="about-the-sensor-class-extension"></a>关于传感器类扩展


为了更轻松地编写向 Windows (和特定) 中的传感器和位置平台公开传感器的设备驱动程序，Windows 包含传感器驱动程序类扩展 [ISensorClassExtension](/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensorclassextension) 接口。 此 COM 对象是传感器设备驱动程序的必备组件，提供一组简单的接口，使程序员无需编写大量样板代码就能够实现传感器驱动程序。 此外，此类扩展提供了以下优势：

-   有助于确保用户隐私受到良好保护，因为类扩展对处理个人信息的传感器强制实施适当的访问控制限制。

-   提供了一种标准方法，用于从驱动程序中检索数据，并通过 API 层引发事件通知。

 

