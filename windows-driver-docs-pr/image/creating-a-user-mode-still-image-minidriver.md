---
title: 创建用户模式静态图像微型驱动程序
description: 创建用户模式静态图像微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8234a9b7bfc4cdba1d3c519ad526d27e3733c33d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820269"
---
# <a name="creating-a-user-mode-still-image-minidriver"></a>创建用户模式静态图像微型驱动程序





所有用户模式静止图像微型驱动程序必须实现 [ISTIUSD COM 接口](istiusd-com-interface.md)定义的接口方法。 此实现相对简单，使用以下过程。

**实现 IStiUSD COM 接口定义的方法：**

1.  获取接口的 GUID，并将其包含在标头文件中，并将安装信息包含 (INF) 文件中。

2.  创建 () 的实现文件。

3.  使用 **IStiUSD** 作为继承类来创建自定义类定义。

4.  实现所有已为 [ISTIUSD COM 接口](istiusd-com-interface.md)定义的方法。 如果不需要某个方法，则该方法必须返回 \_ 不受支持的 STIERR。

本部分提供有关以下主题的信息：

[静态图像设备事件](still-image-device-events.md)

[传输模式](transfer-modes.md)

[静态图像驱动程序的安全问题](security-issues-for-still-image-drivers.md)

 

 




