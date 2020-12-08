---
title: 静态图像驱动程序的安全问题
description: 静态图像驱动程序的安全问题
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: c303e458cac02b36d2af67ed45e09522f51930ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839099"
---
# <a name="security-issues-for-still-image-drivers"></a>静态图像驱动程序的安全问题

请务必记住，可以通过映像获取 API 从应用程序调用用户模式微型驱动程序，也可以从作为 Windows 服务实现的静止图像事件监视器中调用。 存在与这些多个调用源相关联的安全问题。 例如，如果用户模式微型驱动程序通过指定 **NULL** 安全描述符) 来创建使用默认安全描述符 (的 mutex，则不能在从事件监视器调用的微型驱动程序的实例与从映像获取 API 调用的实例之间共享一个互斥体。
