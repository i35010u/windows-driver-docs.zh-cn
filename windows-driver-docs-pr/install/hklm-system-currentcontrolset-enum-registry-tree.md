---
title: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树包含有关系统上的设备的信息。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6539b96c857b9cdee39f061834c10fd6a6cfad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837494"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\枚举注册表树





**枚举**树是保留供操作系统组件使用的，并且其布局可能会更改。 驱动程序和用户模式[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))必须使用系统提供的函数（如[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)和[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)）从此树中提取信息。 *驱动程序和 Windows 应用程序不能直接访问****枚举****树。*

 

 





