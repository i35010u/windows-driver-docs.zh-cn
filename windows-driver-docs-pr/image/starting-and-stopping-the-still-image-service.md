---
title: 启动和停止静态图像服务
description: 启动和停止静态图像服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 953f62146900a54987312406c6b7f0f35975688a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802443"
---
# <a name="starting-and-stopping-the-still-image-service"></a>启动和停止静态图像服务





用户通常不需要启动或停止静止图像服务，但开发人员在安装或卸载驱动程序时必须启动或停止此服务。 可以通过以下两种方式之一来启动和停止静止图像服务：

在命令窗口中发出命令。

若要启动静止图像服务，请发出以下命令：

```console
net start stisvc
```

若要停止静态映像服务，请发出以下命令：

```console
net stop stisvc
```

使用 Microsoft 管理控制台 (MMC) 。

在 " **服务**" 下，选择 " **静止图像服务**"。 若要启动该服务，请右键单击，然后从出现的菜单中单击 " **启动** "。

若要停止该服务，请右键单击，然后在显示的菜单中单击 " **停止** "。
