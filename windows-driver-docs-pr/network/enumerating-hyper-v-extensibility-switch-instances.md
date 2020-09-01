---
title: 枚举 Hyper-V 可扩展交换机实例
description: 枚举 Hyper-V 可扩展交换机实例
ms.assetid: 1C4FE71E-689C-4BE8-BDA8-FFC318E37A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cbc5721627ee7b03735ccc7fa2861654cc24034
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212189"
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

 

