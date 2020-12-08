---
title: 启用 Hyper-V 可扩展交换机扩展
description: 启用 Hyper-V 可扩展交换机扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42209a2805adc1f4f9aef9663fce0f1010fb4463
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822953"
---
# <a name="enabling-hyper-v-extensible-switch-extensions"></a>启用 Hyper-V 可扩展交换机扩展


安装 Hyper-v 可扩展交换机扩展后，它们将绑定到可扩展交换机的每个实例。 但是，默认情况下，这些扩展是禁用的，必须在每个可扩展交换机实例上显式启用。

[VMSwitchExtension](/powershell/module/hyper-v/enable-vmswitchextension) PowerShell cmdlet 可在可扩展交换机的特定实例上启用扩展。 此 cmdlet 使用以下语法：

``` syntax
Enable-VMSwitchExtension [-Name] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Enable-VMSwitchExtension [-Name] <string[]> [-VMSwitchName] <string[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Enable-VMSwitchExtension [-Name] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Enable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>] [<CommonParameters>]
```

下面演示了如何使用 Enable-VMSwitchExtension cmdlet 的示例。

``` syntax
PS C:\Windows\system32> Enable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**注意**  默认情况下，每个可扩展交换机实例上都启用了 Windows 筛选平台 (WFP) 内置筛选扩展 ( # A0 ) 。

 

## <a name="related-topics"></a>相关主题


[VMSwitchExtension](/powershell/module/hyper-v/enable-vmswitchextension)

[VMSwitchExtension](/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm \_ EthernetSwitchExtension**](/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

