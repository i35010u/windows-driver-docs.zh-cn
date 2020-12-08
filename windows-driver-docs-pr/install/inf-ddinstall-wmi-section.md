---
title: INF DDInstall.WMI 节
description: INF DDInstall 部分包含一个或多个 WMIInterface 指令，这些指令为驱动程序提供的每个 WMI 类指定特征。
keywords:
- INF DDInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.WMI Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 515244e04e1e101da518a0fa9529f228fafdce05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787431"
---
# <a name="inf-ddinstallwmi-section"></a>INF DDInstall.WMI 节


INF *DDInstall*。**WMI** 部分包含一个或多个 **WMIInterface** 指令，这些指令为驱动程序提供的每个 WMI 类指定特征。

```inf
[install-section-name.WMI] |
[install-section-name.nt.WMI] | 
[install-section-name.ntx86.WMI] |
[install-section-name.ntarm.WMI] |  (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.WMI]  (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.WMI] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.WMI]  (Windows XP and later versions of Windows)
 
WMIInterface={WmiClassGUID},[flags,]WMI-class-section
```

## <a name="entries"></a>项


<a href="" id="wmiclassguid"></a>*WmiClassGUID*  
指定标识 WMI 类的 GUID 值。

<a href="" id="flags"></a>*随意*  
指定下列位掩码标志之一：

<a href="" id="0x00000001--scwmi-clobber-security-"></a>0x00000001 (SCWMI_CLOBBER_SECURITY)   
如果已设置，并且注册表中已经存在安全描述符，则现有的安全描述符将替换为 INF 文件中指定的安全描述符。 如果未设置，并且注册表中已经存在安全描述符，则使用现有的安全描述符，而不是在 INF 文件中指定的安全描述符。

<a href="" id="wmi-class-section"></a>*WMI-class-部分*  
指定一个 INF 文件部分，其中包含用于设置 WMI 类的特征的指令。

可在 *WMI 类部分* 中指定以下指令：

<a href="" id="security--security-descriptor-string-"></a>**Security = "**<em>security-描述符-string</em>**"**  
指定将存储在注册表中并应用于 *WmiClassGUID* 指定的 GUID 的安全描述符。 此安全描述符指定访问与类关联的数据块所需的权限。 *安全描述符字符串* 值是一个字符串，其标记指示 DACL (**D：**) 安全组件。

只能存在一个 **安全** 条目。 如果存在多个 **安全** 条目，则不会为 WMI 类设置安全性。

<a name="remarks"></a>备注
-------

INF <em>DDInstall</em>**。WMI** 部分在 Microsoft Windows Server 2003 和更高版本的操作系统上可用。

安全描述符与每个 WMI GUID 相关联。 对于 Windows XP 和早期版本的操作系统版本，WMI Guid 的默认安全描述符允许所有用户完全访问。 对于 Windows Server 2003 及更高版本，默认安全描述符仅允许管理员访问。

如果你的驱动程序定义 WMI 类，并且你不希望使用默认描述符，请包含一个 <em>DDInstall</em>**。"WMI** " 部分指定存储在注册表中的安全描述符，并覆盖系统的默认描述符。

有关如何在 INF 文件中指定安全描述符的详细信息，请参阅 [创建安全设备安装](creating-secure-device-installations.md)。

<a name="examples"></a>示例
--------

下面的示例演示了单个 <em>DDInstall</em>**。WMI** 节，其中包含两个 **WMIInterface** 指令。 每个指令标识一个 WMI 类，并为类指定一个 *wmi 类部分* 。

```inf
[InstallA.NT.WMI]
WMIInterface = {99999999-4cf9-11d2-ba4a-00a0c9062910},,WMISecurity1
WMIInterface = {99999998-4cf9-11d2-ba4a-00a0c9062910},1,WMISecurity2

[WmiSecurity1]
security = "O:BAG:BAD:(A;;0x120fff;;;BA)(A;;CC;;;WD)(A;;0x120fff;;;SY)"

[WmiSecurity2]
security = "O:BAG:BAD:(A;;0x120fff;;;BA)(A;;CC;;;WD)(A;;0x120fff;;;SY)"
```

## <a name="see-also"></a>请参阅


[***DDInstall** _](inf-ddinstall-section.md)

[_ *_模型_**](inf-models-section.md)

 

 






