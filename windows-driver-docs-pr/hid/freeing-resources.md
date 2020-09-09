---
title: 释放资源
description: 作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。
ms.assetid: 19cbc443-cc25-448f-92dc-d9586c1fd5a7
keywords:
- 集合 WDK HID，可用资源
- HID 集合 WDK，免费资源
- 释放 HID 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a881160b5aa863cd8d94a9dda1f548a5882223a
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592455"
---
# <a name="freeing-resources"></a>释放资源


作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。




例如，用户模式应用程序必须在为 HIDClass 设备完成初始化和连接操作后，使用从[**SetupDiGetClassDevs**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)获取的设备列表的句柄调用[**SetupDiDestroyDeviceInfoList**](/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist) 。 调用 **SetupDiDestroyDeviceInfoList** 失败会导致内存泄漏。

 

