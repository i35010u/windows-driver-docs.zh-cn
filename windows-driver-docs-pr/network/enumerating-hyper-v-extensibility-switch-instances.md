---
title: 枚举 Hyper-V 可扩展交换机实例
description: 枚举 Hyper-V 可扩展交换机实例
ms.assetid: 1C4FE71E-689C-4BE8-BDA8-FFC318E37A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea881213f36857e49d3afce9ef31fa8dbf3e2ece
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563639"
---
# <a name="enumerating-hyper-v-extensible-switch-instances"></a>枚举 Hyper-V 可扩展交换机实例


[Get-vmswitch](https://technet.microsoft.com/library/hh848499.aspx) PowerShell cmdlet 枚举已创建的 HYPER-V 虚拟网络。 一个或多个 HYPER-V 子分区可以分配给每个虚拟网络。 启动第一个分配给网络的 HYPER-V 子分区时，HYPER-V 虚拟化堆栈创建虚拟网络的 HYPER-V 可扩展交换机的实例。

[Get-vmswitch](https://technet.microsoft.com/library/hh848499.aspx) cmdlet 使用以下语法：

``` syntax
Get-VMSwitch [[-Name] <string>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]

Get-VMSwitch [[-Id] <Guid[]>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]
```

下面的示例演示的输出[Get-vmswitch](https://technet.microsoft.com/library/hh848499.aspx) cmdlet。

``` syntax
PS C:\Windows\system32> Get-VMSwitch

Name                           Learnable Status
                               Addresses
----                           --------- ------
Virtual Network - 1            2048      {OK}
Virtual Network - 2            2048      {OK}
```

## <a name="related-topics"></a>相关主题


[Get-VMSwitch](https://technet.microsoft.com/library/hh848499.aspx)

[**Msvm\_VirtualEthernetSwitch**](https://msdn.microsoft.com/library/hh850242)

 

 






