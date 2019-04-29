---
title: 启动和停止静态图像服务
description: 启动和停止静态图像服务
ms.assetid: 52770566-1d03-4ae8-9925-240fffcc5f57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f4ef05bee8372ad25a4d711ab1475f76aff0ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378074"
---
# <a name="starting-and-stopping-the-still-image-service"></a>启动和停止静态图像服务





用户通常不必启动或停止静止图像服务，但开发人员必须启动或停止此服务，安装或卸载驱动程序时。 你可以启动和停止中通过两种不同的方式的静止图像服务：

在命令窗口中发出命令。

若要启动仍映像服务，请发出以下命令：

```console
net start stisvc
```

若要停止仍映像服务，请发出以下命令：

```console
net stop stisvc
```

使用 Microsoft 管理控制台 (MMC)。

下**Services**，选择**仍图像服务**。 若要启动服务，右键单击，再单击**启动**从显示的菜单。

若要停止服务，右键单击，再单击**停止**从显示的菜单。
