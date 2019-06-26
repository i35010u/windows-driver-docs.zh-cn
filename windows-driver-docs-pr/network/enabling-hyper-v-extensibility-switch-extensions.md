---
title: 启用 Hyper-V 可扩展交换机扩展
description: 启用 Hyper-V 可扩展交换机扩展
ms.assetid: 13FD68CB-8F50-4BE3-8822-03464D8C118C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 971de17905c9f848856088c0e85b21fea2c77cd4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379434"
---
# <a name="enabling-hyper-v-extensible-switch-extensions"></a>启用 Hyper-V 可扩展交换机扩展


当安装 HYPER-V 可扩展交换机扩展时，将它们绑定到可扩展交换机的每个实例。 但是，扩展默认情况下禁用，必须显式启用每个可扩展交换机实例上。

[Enable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/enable-vmswitchextension) PowerShell cmdlet 可启用可扩展交换机的特定实例中的扩展。 此 cmdlet 使用以下语法：

``` syntax
Enable-VMSwitchExtension [-Name] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Enable-VMSwitchExtension [-Name] <string[]> [-VMSwitchName] <string[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Enable-VMSwitchExtension [-Name] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Enable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>] [<CommonParameters>]
```

下面演示如何使用 Enable-vmswitchextension cmdlet 的示例。

``` syntax
PS C:\Windows\system32> Enable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**请注意**  Windows 筛选平台 (WFP) 框中筛选扩展 (Wfplwfs.sys) 默认启用的每个可扩展交换机实例上。

 

## <a name="related-topics"></a>相关主题


[Enable-VMSwitchExtension](https://docs.microsoft.com/powershell/module/hyper-v/enable-vmswitchextension)

[Get-VMSwitchExtension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

 






