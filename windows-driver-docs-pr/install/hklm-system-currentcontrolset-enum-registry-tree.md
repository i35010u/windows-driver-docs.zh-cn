---
title: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树包含有关系统上的设备的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dc5a90e5f94a31aa657fa158cc79f67d575d37e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791751"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM \\ 系统 \\ CurrentControlSet \\ 枚举注册表树





**枚举** 树是保留供操作系统组件使用的，并且其布局可能会更改。 驱动程序和用户模式 [设备安装组件](/previous-versions/ff541277(v=vs.85)) 必须使用系统提供的函数（如 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 和 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)）从此树中提取信息。 *驱动程序和 Windows 应用程序不能访问*  ***枚举** _ 直接 _tree。 *

 

