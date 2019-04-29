---
Description: 选择性挂起升级版本的 Microsoft Windows XP 已禁用。 它可用于 Windows XP、 Windows Vista 和更高版本的 Windows 的干净安装。
title: 启用选择性挂起
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1b913f4206fb1d0eeae890e39f06395bd83ee637
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383023"
---
# <a name="enabling-selective-suspend"></a>启用选择性挂起


选择性挂起升级版本的 Microsoft Windows XP 已禁用。 它可用于 Windows XP、 Windows Vista 和更高版本的 Windows 的干净安装。

若要启用选择性挂起对给定的根中心和其子设备的支持，在选中的复选框**电源管理**USB 根集线器中的选项卡**设备管理器**。

或者，可以启用或禁用选择性暂停的值设置**HcDisableSelectiveSuspend** USB 端口驱动程序软件项下。 值为 1 禁用选择性挂起。 值为 0 允许选择性挂起。

例如，Usbport.inf 禁用选择性中的以下行挂起 Hydra OHCI 控制器：

```cpp
[OHCI_NOSS.AddReg.NT]
HKR,,"HcDisableSelectiveSuspend",0x00010001,1
```

客户端驱动程序不应尝试确定是否选择性挂起发送空闲请求之前已启用。 每当在设备处于空闲状态时，他们应提交空闲状态的请求。 如果空闲状态的请求失败，客户端驱动程序应重置空闲计时器，然后重试。

## <a name="related-topics"></a>相关主题


[USB 选择性挂起](usb-selective-suspend.md)

[USB 电源管理](usb-power-management.md)

 

 





