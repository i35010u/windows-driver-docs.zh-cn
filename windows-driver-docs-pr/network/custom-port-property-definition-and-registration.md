---
title: 自定义端口属性定义和注册
description: 自定义端口属性定义和注册
ms.assetid: 55FCA402-191B-4DC9-A126-77AA15183E90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680731bfb4dc29dbc601cc8433097fe305203c04
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207611"
---
# <a name="custom-port-property-definition-and-registration"></a>自定义端口属性定义和注册


Hyper-v 可扩展交换机端口策略的自定义属性定义通过使用 (MOF) 类定义的托管对象格式注册到 WMI 管理层。 除了定义自定义端口属性的属性的结构成员以外，MOF 类还必须包含以下内容：

-   用于唯一标识自定义端口属性的 UUID。

-   唯一标识可扩展交换机扩展的 GUID。 此 GUID 声明为 MOF 类的 **ExtensionId** 限定符，并且必须与扩展的 INF 文件中声明的 **NetCfgInstanceId** 条目的值匹配。

-   描述性类名字符串。 供应商的名称必须包括在字符串中。

下面显示了可扩展交换机端口策略的自定义属性的 MOF 类的示例。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
 Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevison("0"),
DisplayName("Fabrikam, Inc. Port Settings Friendly Name") : Amended,
Description("Fabrikam, Inc. Port Settings detailed description.") : Amended]
class Fabrikam_PortCustomSettingData : Msvm_EthernetSwitchPortFeatureSettingData {
   
    [ Read,
      Write,
      WmiDataId(1),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int32 setting.") : Amended]
    uint32 SettingIntA = 0;

    [ Read,
      Write,
      WmiDataId(2),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int64 setting.") : Amended]
    uint64 SettingIntB = 0;
};
```

端口策略的自定义属性的 MOF 类通过使用 MOF 编译器 ( # A0) 在通用信息模型中注册 (CIM) 存储库。 注册后，MOF 类可通过 PowerShell cmdlet 和基于 WMI 的应用程序进行配置。

下面的示例演示了必须输入的命令，以注册 \_ 包含自定义端口属性的 mof 类 (Fabrikam PortCustomSettingData) 的文件。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_PortCustomSettingData.mof
net start vmms
```

有关如何使用 MOF 编译器的详细信息，请参阅 [编译驱动程序的 MOF 文件](../kernel/compiling-a-driver-s-mof-file.md)。

下面的示例演示如何配置示例功能。 在此示例中，Fabrikam \_ PORTCUSTOMSETTINGDATA MOF 类用于从名为 "TestVm" 的 hyper-v 分区配置端口。

```PowerShell
# Retrieve the template object for the custom configuration. We know the ID already so
# we can retrieve it directly, otherwise Get-VmSystemSwitchExtensionPortFeature can list all available
# properties. 
PS C:\> $feature = Get-VMSystemSwitchExtensionPortFeature -FeatureId EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB

# Output the values
PS C:\> $feature

Id            : eb29f0f2-f5dc-45c6-81bb-3cd9f219bbbb
ExtensionId   : 5cbf81bd-5055-47cd-9055-a76b2b4e369d
ExtensionName : Fabrican Extension
Name          : Fabrikam, Inc. Port Settings Friendly Name
ComputerName  : TEST_SERVER
SettingData   : \\TEST_SERVER\root\virtualization\v2:VendorName_SwitchPortCustomSettingData.InstanceID="Microsoft:Defini
                tion\\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\\Default"

# Cast the SettingsData to a WMI object to see the actual configurable values. 
PS C:\> $wmiObj = [wmi]$feature.SettingData
PS C:\> $wmiObj

__GENUS          : 2
__CLASS          : Fabrikam_PortCustomSettingData
__SUPERCLASS     : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY        : CIM_ManagedElement
__RELPATH        : Fabrikam_PortCustomSettingData.InstanceID="Microsoft:Definition\\EB29F0F2-F5DC-45C6-81BB-3CD
                   9F219BBBB\\Default"
__PROPERTY_COUNT : 6
__DERIVATION     : {Msvm_EthernetSwitchFeatureSettingData, CIM_SettingData, CIM_ManagedElement}
__SERVER         : TEST_SERVER
__NAMESPACE      : root\virtualization\v2
__PATH           : \\TEST_SERVER\root\virtualization\v2:Fabrikam_PortCustomSettingData.InstanceID="Microsoft:Def
                   inition\\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\\Default"
Caption          : Fabrikam, Inc. Port Settings Friendly Name
Description      : Fabrikam, Inc. Port Settings detailed description.
ElementName      : Fabrikam, Inc. Port Settings Friendly Name
InstanceID       : Microsoft:Definition\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\Default
SettingIntA      : 0
SettingIntB      : 0

# Update the property settings and add to the NIC attached to TestVm
PS C:\> $wmiObj.SettingIntA = 100
PS C:\> $wmiObj.SettingIntB = 9999
PS C:\> Add-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $feature -VmName TestVm
 
# Validate that the properties are now set on the VM’s NIC
PS C:\> $feature = Get-VmSwitchExtensionPortFeature -FeatureId EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB -VmName TestVm

PS C:\> [wmi]$feature.SettingData


__GENUS          : 2
__CLASS          : Fabrikam_PortCustomSettingData
__SUPERCLASS     : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY        : CIM_ManagedElement
__RELPATH        : Fabrikam_PortCustomSettingData.InstanceID="Microsoft:6208FB20-2490-4DC1-B121-877B68B4CE11\\4
                   DDC57F5-6DAE-4A36-9D62-7A838D5601F2\\C\\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\\CB323B56-FA54-4506-B58
                   B-78C70C0B3229"
__PROPERTY_COUNT : 6
__DERIVATION     : {Msvm_EthernetSwitchFeatureSettingData, CIM_SettingData, CIM_ManagedElement}
__SERVER         : TEST_SERVER
__NAMESPACE      : root\virtualization\v2
__PATH           : \\TEST_SERVER\root\virtualization\v2:Fabrikam_PortCustomSettingData.InstanceID="Microsoft:620
                   8FB20-2490-4DC1-B121-877B68B4CE11\\4DDC57F5-6DAE-4A36-9D62-7A838D5601F2\\C\\EB29F0F2-F5DC-45C6-81BB-
                   3CD9F219BBBB\\CB323B56-FA54-4506-B58B-78C70C0B3229"
Caption          : Fabrikam, Inc. Port Settings Friendly Name
Description      : Fabrikam, Inc. Port Settings detailed description.
ElementName      : Fabrikam, Inc. Port Settings Friendly Name
InstanceID       : Microsoft:6208FB20-2490-4DC1-B121-877B68B4CE11\4DDC57F5-6DAE-4A36-9D62-7A838D5601F2\C\EB29F0F2-F5DC-
                   45C6-81BB-3CD9F219BBBB\CB323B56-FA54-4506-B58B-78C70C0B3229
SettingIntA      : 100
SettingIntB      : 9999
```

有关可扩展交换机扩展如何管理端口策略的详细信息，请参阅 [管理端口策略](managing-port-policies.md)。

 

