---
title: 重新排列 Hyper-V 可扩展交换机扩展的顺序
description: 重新排列 Hyper-V 可扩展交换机扩展的顺序
ms.assetid: DAB7FAE0-1632-4FD1-8697-48553A51BD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d25a246b1aa22b1d38d5416c2b1e77e39a762bf7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216588"
---
# <a name="reordering-hyper-v-extensible-switch-extensions"></a>重新排列 Hyper-V 可扩展交换机扩展的顺序


可以在可扩展交换机的每个实例中启用多个 Hyper-v 可扩展交换机捕获或筛选扩展。

**注意**   在可扩展交换机的每个实例中只能启用一个转发扩展。

 

默认情况下，多个捕获或筛选扩展基于其类型和安装时间进行排序。 例如，多个捕获扩展在可扩展交换机驱动程序堆栈中分层，最新安装的扩展与交换机的协议边缘最接近。

安装多个捕获或筛选扩展时，可以使用 PowerShell cmdlet 在可扩展交换机驱动程序堆栈中重新排列驱动程序的顺序。 下面的示例演示了在 PowerShell 窗口中输入的命令。

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


[获取-VMSwitch](/powershell/module/hyper-v/get-vmswitch)

[**Msvm \_ EthernetSwitchExtension**](/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

[**Msvm \_ VirtualEthernetSwitchSettingData**](/windows/desktop/HyperV_v2/msvm-virtualethernetswitchsettingdata)

 

