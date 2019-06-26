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
ms.openlocfilehash: fff45294ae04a7bd055e55e9924aacb7b6d4a15e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381781"
---
# <a name="freeing-resources"></a>释放资源


用户模式应用程序和内核模式驱动程序的 HID 客户端应始终释放不再需要的任何资源。




例如，在用户模式应用程序必须调用[ **SetupDiDestroyDeviceInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist)句柄从它获取设备列表[ **SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) HIDClass 设备及其初始化和连接操作完成后。 调用失败**SetupDiDestroyDeviceInfoList**会导致内存泄漏。

 

 




