---
title: 静态图像驱动程序
description: 静态图像驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: babc923334f0261589c448c26a611ff77310eddf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792861"
---
# <a name="still-image-drivers"></a>静态图像驱动程序





Microsoft Windows 驱动程序工具包 (WDK) 包含一个名为 "Windows 映像采集 (WIA) " 的体系结构。 WIA 建立在 microsoft STI) 的 Microsoft 静止映像体系 (结构基础之上，因此 STI 上构建的驱动程序可轻松迁移到 WIA。

本部分针对在 Microsoft STI 上开发的旧驱动程序提供。 它介绍了 Microsoft STI 定义的 COM 接口，并将此类静止图像硬件供应商提供给平板扫描仪和数字静止图像相机。 本部分中描述的 COM 接口由以下供应商提供的软件由或定义。

-   图像采集 API 软件的设备特定组件（如 TWAIN 数据源，这些组件是必需的，因此 TWAIN API 可以支持特定的静止图像设备）。

-   用户模式静止图像微型驱动程序，提供从图像采集软件到低级设备和总线驱动程序的通信路径。

部分包含以下部分：

[Microsoft STI 和 Microsoft WIA 概述](overview-of-microsoft-sti-and-microsoft-wia.md)

[Microsoft STI 简介](introduction-to-microsoft-sti.md)

[Microsoft STI 组件](microsoft-sti-components.md)

[静态图像 COM 接口](still-image-com-interfaces.md)

[创建推送模型感知应用程序](creating-push-model-aware-applications.md)

[为图像采集 API 创建特定于设备的组件](creating-device-specific-components-for-image-acquisition-apis.md)

[创建用户模式静态图像微型驱动程序](creating-a-user-mode-still-image-minidriver.md)

[安装和配置静态图像组件](installing-and-configuring-still-image-components.md)

[启动和停止静态图像服务](starting-and-stopping-the-still-image-service.md)

[调试静态图像组件](debugging-still-image-components.md)

 

 




