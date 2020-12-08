---
title: 枚举 Hyper-V 可扩展交换机实例
description: 枚举 Hyper-V 可扩展交换机实例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a2e8ae43cc51883fb5c24b9b11315f71cd88199
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823919"
---
# <a name="enumerating-hyper-v-extensible-switch-instances"></a>枚举 Hyper-V 可扩展交换机实例


" [获取-VMSwitch](/powershell/module/hyper-v/get-vmswitch) " PowerShell cmdlet 枚举已创建的 hyper-v 虚拟网络。 可以为每个虚拟网络分配一个或多个 Hyper-v 子分区。 当分配给网络的第一个 Hyper-v 子分区启动时，Hyper-v 虚拟化堆栈为虚拟网络创建 Hyper-v 可扩展交换机的实例。

[获取-VMSwitch](/powershell/module/hyper-v/get-vmswitch) cmdlet 使用以下语法：

``` syntax
Get-VMSwitch [[-Name] <string>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]

Get-VMSwitch [[-Id] <Guid[]>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]
```

下面的示例演示了 [获取-VMSwitch](/powershell/module/hyper-v/get-vmswitch) cmdlet 的输出。

``` syntax
PS C:\Windows\system32> Get-VMSwitch

Name                           Learnable Status
                               Addresses
----                           --------- ------
Virtual Network - 1            2048      {OK}
Virtual Network - 2            2048      {OK}
```

## <a name="related-topics"></a>相关主题


[获取-VMSwitch](/powershell/module/hyper-v/get-vmswitch)

[**Msvm \_ VirtualEthernetSwitch**](/windows/desktop/HyperV_v2/msvm-virtualethernetswitch)

 

