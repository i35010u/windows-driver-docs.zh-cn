---
title: 重新排列 Hyper-V 可扩展交换机扩展的顺序
description: 重新排列 Hyper-V 可扩展交换机扩展的顺序
ms.assetid: DAB7FAE0-1632-4FD1-8697-48553A51BD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e315791f501d11e65a513e808b70a0e3ace6c4ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373291"
---
# <a name="reordering-hyper-v-extensible-switch-extensions"></a>重新排列 Hyper-V 可扩展交换机扩展的顺序


可以在可扩展交换机的每个实例中启用多个 HYPER-V 可扩展交换机捕获或筛选扩展。

**请注意**  只有一个转发扩展可以在可扩展交换机的每个实例中启用。

 

默认情况下，多个捕获或筛选扩展排序基于它们的类型上和安装它们。 例如，多个捕获扩展的分层中具有最新安装的扩展的交换机的协议边缘最接近的可扩展交换机驱动程序堆栈。

当安装了多个捕获或筛选扩展时，可以使用 PowerShell cmdlet 对可扩展交换机驱动程序堆栈中的驱动程序进行重新排序。 下面的示例显示了要执行此操作的 PowerShell 窗口中输入的命令。

``` syntax
# Show the current order. The ExtensionOrder field contains paths to WMI extension instances.
# The [wmi] operator can be used to convert the paths to full WMI objects. 
PS C:\Windows\system32> $privateNetwork = Get-VMSwitch PrivateNetwork
PS C:\Windows\system32> $extensionOrder = $privateNetwork.ExtensionOrder
PS C:\Windows\system32> $extensionOrder | ForEach-Object { Write-Host "Name:" ([wmi]$_).ElementName }
Name: NDIS Capture LightWeight Filter
Name: Switch Extensibility Test Extension 2
Name: Switch Extensibility Test Extension 1
Name: WFP extensible switch Layers LightWeight Filter

# Place “Test Extension 1” above “Test Extension 2” in the ordered list of extensions.
PS C:\Windows\system32> $tmp = $extensionOrder[1]
PS C:\Windows\system32> $extensionOrder[1] = $extensionOrder[2]
PS C:\Windows\system32> $extensionOrder[2] = $tmp

# Commit the updated order.
PS C:\Windows\system32> $privateNetwork.ExtensionOrder = $extensionOrder

# Retrieve the switch information again to validate the order.
PS C:\Windows\system32> $privateNetwork = Get-VMSwitch PrivateNetwork
PS C:\Windows\system32> $privateNetwork.ExtensionOrder | ForEach-Object { Write-Host "Name:" ([wmi]$_).ElementName }
Name: NDIS Capture LightWeight Filter
Name: Switch Extensibility Test Extension 1
```

## <a name="related-topics"></a>相关主题


[Get-VMSwitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

[**Msvm\_VirtualEthernetSwitchSettingData**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-virtualethernetswitchsettingdata)

 

 






