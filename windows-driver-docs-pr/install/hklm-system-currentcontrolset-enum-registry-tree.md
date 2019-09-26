---
title: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树包含有关系统上的设备的信息。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 554502e440a88e3cb0915daa4ee8771a7bb4e43c
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278368"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\系统\\CurrentControlSet\\枚举注册表树





**枚举**树是保留供操作系统组件使用的，并且其布局可能会更改。 驱动程序和用户模式[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))必须使用系统提供的函数（如[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)和[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)）从此树中提取信息。 *驱动程序和 Windows 应用程序不能访问****枚举****树。*

 

 





