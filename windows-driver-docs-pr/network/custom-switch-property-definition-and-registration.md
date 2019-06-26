---
title: 自定义交换机属性定义和注册
description: 自定义交换机属性定义和注册
ms.assetid: DB80E86D-8553-47B5-8AE1-6D430FDDE206
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b206b4d578d3cce6e235fabf53da6bd74cb82df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364953"
---
# <a name="custom-switch-property-definition-and-registration"></a>自定义交换机属性定义和注册


HYPER-V 可扩展交换机策略的自定义属性定义使用的托管的对象格式 (MOF) 类定义来注册使用 WMI 管理层。 除了定义的自定义开关属性特性的结构成员、 MOF 类还必须包含以下：

-   唯一标识自定义开关属性 UUID。

-   用于唯一标识此可扩展交换机扩展的 GUID。 此 GUID 声明为**ExtensionId**限定符 MOF 的类，并且必须匹配的值**NetCfgInstanceId**扩展的 INF 文件中声明的项。

-   描述性类名称字符串。 必须在字符串中包含的供应商的名称。

下面显示了一个可扩展交换机策略的自定义属性的 MOF 类的示例。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("FF36C3A6-D2F1-46ed-A376-32B43D6B8390"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
  Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevison("0"),
DisplayName("Fabrikam, Inc.  Switch Settings Friendly Name") : Amended,
Description("Fabrikam, Inc.  Switch Settings detailed description.") : Amended]
class Fabrikam_SwitchCustomSettingData : Msvm_EthernetSwitchFeatureSettingData {
   
    [ Read,
      Write,
      WmiDataId(1),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int32 setting.") : Amended]
    uint32 SwitchSettingIntA = 0;

    [ Read,
      Write,
      WmiDataId(2),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int64 setting.") : Amended]
    uint64 SwitchSettingIntB = 0;
};
```

切换策略的自定义属性的 MOF 类通用信息模型 (CIM) 存储库中注册使用 MOF 编译器 (Mofcomp.exe)。 注册后，可以通过 PowerShell cmdlet 和基于 WMI 的应用程序配置 MOF 类。

下面的示例演示必须输入要注册文件的命令 (Fabrikam\_SwitchCustomSettingData.mof)，其中包含的 MOF 类的自定义端口属性。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_SwitchCustomSettingData.mof
net start vmms
```

有关如何使用 MOF 编译器的详细信息，请参阅[编译的驱动程序的 MOF 文件](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)。

下面的示例演示如何配置示例功能。 在此示例中，Fabrikam\_SwitchCustomSettingData MOF 类用于配置名为"TestSwitch"的交换机。

```PowerShell
# Retrieve the template object for the custom configuration. We know the ID already so
# we can retrieve it directly, otherwise Get-VMSystemSwitchExtensionSwitchFeature can list all available
# properties. 
PS C:\> $feature = Get-VMSystemSwitchExtensionSwitchFeature -FeatureId FF36C3A6-D2F1-46ed-A376-32B43D6B8390

# Output the values
PS C:\temp> $feature


Id            : ff36c3a6-d2f1-46ed-a376-32b43d6b8390
ExtensionId   : 5CBF81BE-5055-47CD-9055-A76B2B4E369E
ExtensionName : Fabrican Extension
Name          : Fabrikam, Inc. Switch Settings Friendly Name
ComputerName  : TEST_SERVER
SettingData   : \\TEST_SERVER\root\virtualization\v2:VendorName_SwitchCustomSettingData.InstanceID="Microsoft:Definition\\
                FF36C3A6-D2F1-46ED-A376-32B43D6B8390\\Default"

# Cast the SettingsData to a WMI object to see the actual configurable values. 
PS C:\> $wmiObj = [wmi]$feature.SettingData
PS C:\> $wmiObj


__GENUS           : 2
__CLASS           : Fabrikam_SwitchCustomSettingData 
__SUPERCLASS      : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY         : CIM_ManagedElement
__RELPATH         : Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:Definition\\FF36C3A6-D2F1-46ED-A376-32B43D
                    6B8390\\Default"
__PROPERTY_COUNT  : 6
__DERIVATION      : {Msvm_EthernetSwitchFeatureSettingData, Msvm_FeatureSettingData, CIM_SettingData,
                    CIM_ManagedElement}
__SERVER          : TEST_SERVER
__NAMESPACE       : root\virtualization\v2
__PATH            : \\TEST_SERVER\root\virtualization\v2:Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:Definiti
                    on\\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\\Default"
Caption           : Fabrikam, Inc. Switch Settings Friendly Name
Description       : Fabrikam, Inc. Switch Settings detailed description.
ElementName       : Fabrikam, Inc. Switch Settings Friendly Name
InstanceID        : Microsoft:Definition\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\Default
SwitchSettingIntA : 0
SwitchSettingIntB : 0
PSComputerName    : TEST_SERVER

# Update the property settings and add to the NIC attached to TestVm
PS C:\> $wmiObj.SwitchSettingIntA = 100
PS C:\> $wmiObj.SwitchSettingIntB = 9999
PS C:\> Add-VMSwitchExtensionSwitchFeature -VMSwitchExtensionFeature $feature -SwitchName TestSwitch
 
# Validate that the properties are now set on the VM’s NIC
PS C:\> $feature = Get-VmSwitchExtensionSwitchFeature -FeatureId FF36C3A6-D2F1-46ed-A376-32B43D6B8390 -SwitchName TestSwitch

PS C:\> [wmi]$feature.SettingData


__GENUS           : 2
__CLASS           : Fabrikam_SwitchCustomSettingData 
__SUPERCLASS      : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY         : CIM_ManagedElement
__RELPATH         : Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:88835394-FDE1-437C-B249-D840575154E2\\FF36
                    C3A6-D2F1-46ED-A376-32B43D6B8390\\F9EA07E7-7B73-431A-8705-26EC2B592306"
__PROPERTY_COUNT  : 6
__DERIVATION      : {Msvm_EthernetSwitchFeatureSettingData, Msvm_FeatureSettingData, CIM_SettingData,
                    CIM_ManagedElement}
__SERVER          : TEST_SERVER
__NAMESPACE       : root\virtualization\v2
__PATH            : \\TEST_SERVER\root\virtualization\v2:Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:88835394
                    -FDE1-437C-B249-D840575154E2\\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\\F9EA07E7-7B73-431A-8705-26EC2B5
                    92306"
Caption           : Fabrikam, Inc. Switch Settings Friendly Name
Description       : Fabrikam, Inc. Switch Settings detailed description.
ElementName       : Fabrikam, Inc. Switch Settings Friendly Name
InstanceID        : Microsoft:88835394-FDE1-437C-B249-D840575154E2\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\F9EA07E7-7B73-4
                    31A-8705-26EC2B592306
SwitchSettingIntA : 100
SwitchSettingIntB : 9999
PSComputerName    : TEST_SERVER
```

有关详细信息如何可扩展交换机扩展管理交换机策略，请参阅[管理切换策略](managing-switch-policies.md)。

 

 





