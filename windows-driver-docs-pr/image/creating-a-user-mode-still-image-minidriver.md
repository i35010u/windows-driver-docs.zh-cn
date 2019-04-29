---
title: 创建用户模式静态图像微型驱动程序
description: 创建用户模式静态图像微型驱动程序
ms.assetid: 94fdbeba-5b4a-4b66-b381-ec362b6d38c9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068de4dc8ed2378faa264b569d8f39e5714a5455
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386320"
---
# <a name="creating-a-user-mode-still-image-minidriver"></a>创建用户模式静态图像微型驱动程序





所有用户模式下仍映像微型驱动程序必须都实现接口方法由定义[IStiUSD COM 接口](istiusd-com-interface.md)。 此实现是相对简单，使用以下过程。

**若要实现由 IStiUSD COM 接口定义的方法：**

1.  获取 GUID 的接口，并将其包含在标头文件和安装信息 (INF) 文件中。

2.  创建实现文件 (.cpp) 等。

3.  创建自定义的类定义，使用**IStiUSD**作为继承的类。

4.  实现的所有已定义的方法[IStiUSD COM 接口](istiusd-com-interface.md)。 如果不需要一种方法，它必须返回 STIERR\_不受支持。

本部分提供有关以下主题的信息：

[静止图像的设备事件](still-image-device-events.md)

[传输模式](transfer-modes.md)

[仍映像驱动程序的安全问题](security-issues-for-still-image-drivers.md)

 

 




