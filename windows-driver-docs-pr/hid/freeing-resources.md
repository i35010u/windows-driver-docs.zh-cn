---
title: 释放资源
description: 用户模式应用程序和内核模式驱动程序的 HID 客户端应始终释放不再需要的任何资源。
ms.assetid: 19cbc443-cc25-448f-92dc-d9586c1fd5a7
keywords:
- WDK HID，可用的资源的集合
- HID 的集合 WDK，可用的资源
- 释放 HID 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4cd26f4b348619b7d200bf9b47eec7b12787d8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378799"
---
# <a name="freeing-resources"></a>释放资源


用户模式应用程序和内核模式驱动程序的 HID 客户端应始终释放不再需要的任何资源。




例如，在用户模式应用程序必须调用[ **SetupDiDestroyDeviceInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550996)句柄从它获取设备列表[ **SetupDiGetClassDevs**](https://msdn.microsoft.com/library/windows/hardware/ff551069) HIDClass 设备及其初始化和连接操作完成后。 调用失败**SetupDiDestroyDeviceInfoList**会导致内存泄漏。

 

 




