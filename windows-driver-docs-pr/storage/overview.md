---
title: 关于存储接收器驱动程序
description: 关于存储接收器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 945ee68ca0e911c664f491b163484e2acd592f20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830959"
---
# <a name="about-storage-silo-drivers"></a>关于存储接收器驱动程序

本部分介绍存储接收器驱动程序系统组件的基础设计和体系结构，这些组件启用以下事件序列：

1. 用户将符合 IEEE 1667 的存储设备连接到其系统。

2. 设备已被识别。 安装并配置了相应的驱动程序、系统组件和第三方组件。

3. Windows shell 和任何已安装的第三方应用程序都可以根据 IEEE 1667 规范来发现、访问和管理设备并与之交互。
