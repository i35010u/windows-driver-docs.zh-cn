---
title: 静态图像驱动程序
description: 静态图像驱动程序
ms.assetid: e207f76e-ff35-4a0d-a4bf-744931055eb8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0792f031ff8962d849cac0c0d960796db67e2b08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364353"
---
# <a name="still-image-drivers"></a>静态图像驱动程序





Microsoft Windows Driver Kit (WDK) 包括名为 Windows 图像采集 (WIA) 的体系结构。 Microsoft 仍映像体系结构 (Microsoft STI) 的基础上构建 WIA，因此将驱动程序轻松地基于 STI 迁移到 WIA。

本部分提供 Microsoft STI 上开发的旧驱动程序。 它描述是由 Microsoft STI 定义和提供的此类静止图像硬件供应商给如平板扫描仪和数字静止图像的相机的 COM 接口。 在本部分中所述的 COM 接口，由调用，或者定义的供应商提供的以下软件：

-   图像 API 获取软件，如需要，以使 TWAIN API 可支持特定静止图像设备 TWAIN 数据源的特定于设备的组件。

-   用户模式下仍映像微型驱动程序，它们提供了从图像获取软件到较低级别设备和总线驱动程序的通信路径。

部分包含以下各节：

[Microsoft STI 和 Microsoft WIA 概述](overview-of-microsoft-sti-and-microsoft-wia.md)

[Microsoft STI 简介](introduction-to-microsoft-sti.md)

[Microsoft STI 组件](microsoft-sti-components.md)

[静止图像的 COM 接口](still-image-com-interfaces.md)

[创建推送模型识别应用程序](creating-push-model-aware-applications.md)

[为图像采集 Api 创建特定于设备的组件](creating-device-specific-components-for-image-acquisition-apis.md)

[创建用户模式下仍映像微型驱动程序](creating-a-user-mode-still-image-minidriver.md)

[安装和配置仍映像组件](installing-and-configuring-still-image-components.md)

[启动和停止静止图像服务](starting-and-stopping-the-still-image-service.md)

[调试仍映像组件](debugging-still-image-components.md)

 

 




