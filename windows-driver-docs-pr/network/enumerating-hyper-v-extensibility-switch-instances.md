---
title: 枚举 Hyper-V 可扩展交换机实例
description: 枚举 Hyper-V 可扩展交换机实例
ms.assetid: 1C4FE71E-689C-4BE8-BDA8-FFC318E37A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15997e27d231ecce3ee179c8c71102900561f327
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379424"
---
# <a name="enumerating-hyper-v-extensible-switch-instances"></a>枚举 Hyper-V 可扩展交换机实例


[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch) PowerShell cmdlet 枚举已创建的 HYPER-V 虚拟网络。 一个或多个 HYPER-V 子分区可以分配给每个虚拟网络。 启动第一个分配给网络的 HYPER-V 子分区时，HYPER-V 虚拟化堆栈创建虚拟网络的 HYPER-V 可扩展交换机的实例。

[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch) cmdlet 使用以下语法：

``` syntax
Get-VMSwitch [[-Name] <string>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]

Get-VMSwitch [[-Id] <Guid[]>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]
```

下面的示例演示的输出[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch) cmdlet。

``` syntax
PS C:\Windows\system32> Get-VMSwitch

Name                           Learnable Status
                               Addresses
----                           --------- ------
Virtual Network - 1            2048      {OK}
Virtual Network - 2            2048      {OK}
```

## <a name="related-topics"></a>相关主题


[Get-VMSwitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch)

[**Msvm\_VirtualEthernetSwitch**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-virtualethernetswitch)

 

 






