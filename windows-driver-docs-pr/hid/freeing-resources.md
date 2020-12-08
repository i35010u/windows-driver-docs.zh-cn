---
title: 释放资源
description: 作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。
keywords:
- 集合 WDK HID，可用资源
- HID 集合 WDK，免费资源
- 释放 HID 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 376f476d90622f221cd7619633e58b2585570674
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838917"
---
# <a name="freeing-resources"></a>释放资源


作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。




例如，用户模式应用程序必须在为 HIDClass 设备完成初始化和连接操作后，使用从 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw)获取的设备列表的句柄调用 [**SetupDiDestroyDeviceInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist) 。 调用 **SetupDiDestroyDeviceInfoList** 失败会导致内存泄漏。

 

