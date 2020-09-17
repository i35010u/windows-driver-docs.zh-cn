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
ms.openlocfilehash: 77b97f1d1d6d326f53465e179af657cb1b30e675
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715966"
---
# <a name="freeing-resources"></a>释放资源


作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。




例如，用户模式应用程序必须在为 HIDClass 设备完成初始化和连接操作后，使用从[**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw)获取的设备列表的句柄调用[**SetupDiDestroyDeviceInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist) 。 调用 **SetupDiDestroyDeviceInfoList** 失败会导致内存泄漏。

 

