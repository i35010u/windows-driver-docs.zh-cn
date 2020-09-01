---
title: 枚举 Hyper-V 可扩展交换机扩展
description: 枚举 Hyper-V 可扩展交换机扩展
ms.assetid: AC468A8F-5C48-419B-9E9E-D63925E1CE9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab7e003905b78d1f0ffcda2b657a63dc788150b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209747"
---
# <a name="enumerating-hyper-v-extensible-switch-extensions"></a>枚举 Hyper-V 可扩展交换机扩展


[VMSwitchExtension](/powershell/module/hyper-v/get-vmsystemswitchextension) PowerShell cmdlet 枚举当前绑定到可扩展交换机的实例的 hyper-v 可扩展交换机扩展。 此 cmdlet 还报告是否在可扩展交换机实例中启用了扩展。

[VMSwitchExtension](/powershell/module/hyper-v/get-vmsystemswitchextension) cmdlet 使用以下语法：

``` syntax
Get-VMSwitchExtension [[-VMSwitchName] <string[]>] [[-Name] <string[]>] [-ComputerName <string[]>]
    [<CommonParameters>]

Get-VMSwitchExtension [[-VMSwitch] <VMSwitch[]>] [-ComputerName <string[]>] [<CommonParameters>]
```

下面的示例演示了 [VMSwitchExtension](/powershell/module/hyper-v/get-vmsystemswitchextension) cmdlet 的输出。

``` syntax
PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : NDIS Capture LightWeight Filter
ExtensionType : Capture
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 2
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : WFP extensible switch Layers LightWeight Filter
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**注意**   为了最大限度地减少信息量，示例通过筛选器命令 "fl" 管道返回的扩展对象。 这将导致显示与 **-property** 开关的特性匹配的部分信息。

 

## <a name="related-topics"></a>相关主题


[VMSwitchExtension](/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm \_ EthernetSwitchExtension**](/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

