---
title: 静态图像驱动程序的安全问题
description: 静态图像驱动程序的安全问题
ms.assetid: ad795cf0-8bff-4b9b-ac43-94c74cc19d60
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 74890262952d804bef97e64a814c159b197a92f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356203"
---
# <a name="security-issues-for-still-image-drivers"></a>静态图像驱动程序的安全问题

请务必记住从应用程序的整个图像采集 API，或作为 Windows 服务实现的静止图像事件监视器，可以调用用户模式下微型驱动程序。 没有与这些多个调用源相关联的安全隐患。 例如，如果用户模式下微型驱动程序创建互斥体使用的默认安全描述符 (通过指定**NULL**安全描述符)，不能从事件监视器调用微型驱动程序的实例之间共享一个互斥锁其中一个名为映像收购 API 中。
