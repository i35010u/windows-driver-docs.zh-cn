---
title: 关于传感器类扩展
description: 关于传感器类扩展
ms.assetid: 4b55e5fe-2947-4511-ba2d-479d5fd83ebe
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a540856abf97e7eccf22a42e1b79951e7c15d70d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842373"
---
# <a name="about-the-sensor-class-extension"></a>关于传感器类扩展


为了更轻松地编写向 Windows 公开传感器的设备驱动程序（特别是传感器和位置平台），Windows 包含传感器驱动程序类扩展， [ISensorClassExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensorclassextension)接口。 传感器设备驱动程序的必需组件提供一组简单的接口，使程序员能够实现传感器驱动程序，而无需编写大量的样板代码。 此外，此类扩展提供了以下优势：

-   有助于确保用户隐私受到良好保护，因为类扩展对处理个人信息的传感器强制实施适当的访问控制限制。

-   提供了一种标准方法，用于从驱动程序中检索数据，并通过 API 层引发事件通知。

 

 




