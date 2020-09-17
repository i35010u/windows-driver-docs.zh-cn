---
title: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树包含有关系统上的设备的信息。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a3980af15ef1144d74874bfa0a4be42bfb928f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717022"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM \\ 系统 \\ CurrentControlSet \\ 枚举注册表树





**枚举**树是保留供操作系统组件使用的，并且其布局可能会更改。 驱动程序和用户模式 [设备安装组件](/previous-versions/ff541277(v=vs.85)) 必须使用系统提供的函数（如 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 和 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)）从此树中提取信息。 *驱动程序和 Windows 应用程序不能直接访问****枚举****树。*

 

