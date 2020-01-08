---
title: 关于存储接收器驱动程序
description: 关于存储接收器驱动程序
ms.assetid: e150228e-820f-49ac-bc3f-644e77f3d544
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eae47543610473920c9deb799ef6a34e28089a7e
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606521"
---
# <a name="about-storage-silo-drivers"></a>关于存储接收器驱动程序

本部分介绍存储接收器驱动程序系统组件的基础设计和体系结构，这些组件启用以下事件序列：

1. 用户将符合 IEEE 1667 的存储设备连接到其系统。

2. 设备已被识别。 安装并配置了相应的驱动程序、系统组件和第三方组件。

3. Windows shell 和任何已安装的第三方应用程序都可以根据 IEEE 1667 规范来发现、访问和管理设备并与之交互。
