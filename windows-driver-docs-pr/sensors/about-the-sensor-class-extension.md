---
title: 关于传感器类扩展
description: 关于传感器类扩展
ms.assetid: 4b55e5fe-2947-4511-ba2d-479d5fd83ebe
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c65fc0c7a575726069bf270b99954f7af89d686
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010149"
---
# <a name="about-the-sensor-class-extension"></a>关于传感器类扩展


为了更轻松地编写向 Windows (和特定) 中的传感器和位置平台公开传感器的设备驱动程序，Windows 包含传感器驱动程序类扩展 [ISensorClassExtension](/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensorclassextension) 接口。 传感器设备驱动程序的必需组件提供一组简单的接口，使程序员能够实现传感器驱动程序，而无需编写大量的样板代码。 此外，此类扩展提供了以下优势：

-   有助于确保用户隐私受到良好保护，因为类扩展对处理个人信息的传感器强制实施适当的访问控制限制。

-   提供了一种标准方法，用于从驱动程序中检索数据，并通过 API 层引发事件通知。

 

