---
title: INF DDInstall.WMI 节
description: INF DDInstall.WMI 部分包含一个或多个指定的驱动程序提供了每个 WMI 类的特征的 WMIInterface 指令。
ms.assetid: 8c4f6b2b-c2b4-4579-9dce-4436e041ebbc
keywords:
- INF DDInstall.WMI 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.WMI Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f02b590e141faf4a96dc6aef12d4bafdd19cb15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370579"
---
# <a name="inf-ddinstallwmi-section"></a>INF DDInstall.WMI 节


INF *DDInstall*。**WMI**部分包含一个或多个**WMIInterface**指定驱动程序提供了每个 WMI 类的特征的指令。

```ini
[install-section-name.WMI] |
[install-section-name.nt.WMI] | 
[install-section-name.ntx86.WMI] |
[install-section-name.ntarm.WMI] |  (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.WMI]  (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.WMI] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.WMI]  (Windows XP and later versions of Windows)
 
WMIInterface={WmiClassGUID},[flags,]WMI-class-section
```

## <a name="entries"></a>条目


<a href="" id="wmiclassguid"></a>*WmiClassGUID*  
指定用于标识 WMI 类的 GUID 值。

<a href="" id="flags"></a>*flags*  
指定以下位掩码标志之一：

<a href="" id="0x00000001--scwmi-clobber-security-"></a>0X00000001 (SCWMI_CLOBBER_SECURITY)  
如果设置，并且如果在注册表中已存在的安全描述符，现有的安全描述符替换为一个 INF 文件中指定。 如果未设置，并且如果在注册表中已存在的安全描述符，而不是 INF 文件中指定的一个使用现有的安全描述符。

<a href="" id="wmi-class-section"></a>*WMI 类部分*  
指定一个 INF 文件部分，其中包含用于设置 WMI 类的特征指令。

在中指定以下指令*WMI 类部分*:

<a href="" id="security--security-descriptor-string-"></a>**Security="**<em>security-descriptor-string</em>**"**  
指定将存储在注册表中并应用于由指定的 GUID 的安全描述符*WmiClassGUID*。 此安全说明符指定所需的访问的数据块与类关联的权限。 *安全描述符字符串*值是指示 DACL 标记的字符串 (**d:**) 安全组件。

只有一个**安全**条目可以出现。 如果多个**安全**条目存在，安全未设置 WMI 类。

<a name="remarks"></a>备注
-------

INF <em>DDInstall</em>**。WMI**部分是 Microsoft Windows Server 2003 和更高版本的操作系统上可用。

安全描述符是与每个 WMI GUID 相关联。 对于 Windows XP 和早期操作系统版本，WMI Guid 的默认安全描述符允许完全访问权限的所有用户。 对于 Windows Server 2003 和更高版本，默认安全描述符允许仅对管理员的访问。

如果您的驱动程序定义的 WMI 类，并且不希望使用默认的描述符，包括<em>DDInstall</em>**。WMI**部分以指定存储在注册表中，重写系统的默认描述符的安全描述符。

有关如何在 INF 文件中指定安全描述符的详细信息，请参阅[创建安全的设备安装](creating-secure-device-installations.md)。

<a name="examples"></a>示例
--------

下面的示例演示单个<em>DDInstall</em>**。WMI**节，其中包含两个**WMIInterface**指令。 每个指令标识 WMI 类，并指定*WMI 类部分*类。

```ini
[InstallA.NT.WMI]
WMIInterface = {99999999-4cf9-11d2-ba4a-00a0c9062910},,WMISecurity1
WMIInterface = {99999998-4cf9-11d2-ba4a-00a0c9062910},1,WMISecurity2

[WmiSecurity1]
security = "O:BAG:BAD:(A;;0x120fff;;;BA)(A;;CC;;;WD)(A;;0x120fff;;;SY)"

[WmiSecurity2]
security = "O:BAG:BAD:(A;;0x120fff;;;BA)(A;;CC;;;WD)(A;;0x120fff;;;SY)"
```

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[***模型***](inf-models-section.md)

 

 






