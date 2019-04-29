---
title: 一对多 ID 映射
description: 一对多 ID 映射
ms.assetid: 395d3f20-7410-496b-9ec3-1052cd731ae3
keywords:
- 映射网络组件 Id
- ID 映射 WDK netmap.inf
- 一个多 ID 映射 WDK 网络
- 升级前 Id WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f00afe01ebf2b07208652a2eda65b56505901805
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384230"
---
# <a name="one-to-many-id-mapping"></a>一对多 ID 映射





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

一个多 ID 映射会在表示多个网络适配器的单一升级前 ID。 区分与单个的升级前 ID 相关联的适配器的唯一方法是检查包含网络适配器实例的参数值的注册表项下的值。

中的条目**OemAdapters**或**OemAsyncAdapters**节指定一个多 ID 映射具有以下格式：

*preupgrade ID* = *映射方法编号*，*节名称*

其中：

*映射方法数*必须为 0

*节名称*包含映射信息在 netmap.inf 文件中指定的部分

通过指定 netmap.inf 文件节*节名称*包含以下各项：

**ValueName = "**<em>Name</em>**"**

指定 NetSetup 读取包含网络适配器实例的参数值的注册表项下的值。 *名称*标识特定网络适配器。

**ValueType =** *Type*

指定的注册表值类型*ValueName*。 *类型*是一个整数，对应于特定的注册表类型。

*ValueName*= *postupgrade-ID*

*ValueName*是 NetSetup 读取包含网络适配器实例的参数值的注册表项下的值。 *postupgrade ID*是 Windows 2000 或更高版本的设备 ID 的适配器。 一个*ValueName*条目应提供有关将升级每个适配器类型。 如果*ValueName*设置为关键字**ValueNotPresent** NetSetup NetSetup 的适配器实例中不找到任何参数值，如果使用*postuprgrade ID*与相关联**ValueNotPresent**适配器。

下面的示例显示了一个多设备 ID 映射：

```cpp
[OemAdapters]
DATAFIREU=0, DATAFIREU

[DATAFIREU]
ValueName  = "BoardType"
ValueType  = 1
DataFireIsaU = "DATAFIRE - ISA1U"
DataFireIsa1ST= "DATAFIRE - ISA1ST"
DataFireIsa4ST= "DATAFIRE - ISA4ST"
DataFireIsaGeneric = "ValueNotPresent"
```

**OemAdapters**在上面的示例部分包含单个条目，用于标识为 DATAFIREU 的网络适配器的升级前的设备 ID 并指定**DATAFIREU**部分netmap.inf 文件包含此适配器的映射信息。

DATAFIREU 部分包含以下信息：

-   **ValueName**项指示要查找的 NetSetup **BoardType**值下**参数**网络适配器实例的密钥。

-   **ValueType**条目，设置为 1，指定**BoardType**值为 dword 值。

-   每个剩余的值指定的升级前的设备 ID 和相应的 Windows 2000 或更高版本的 id。 例如，DataFireIsaU 板类型的 ID 是 DATAFIRE-ISA1U。 **ValueNotPresent**关键字可以指定而不是升级前的 id。

NetSetup 执行一个多 ID 映射，如下所示：

1.  NetSetup 读取包含网络适配器实例的参数值的注册表项下指定的 ValueName。

2.  NetSetup 尝试匹配与一个 netmap.inf 文件的指定部分中列出 ValueNames ValueName。 如果没有 ValueName 下列出的注册表项，NetSetup 尝试 netmap.inf 文件的指定部分中找到 ValueNotPresent 关键字。

3.  如果 NetSetup 找到的匹配项，则会安装网络适配器，使用 INF 文件具有相同的名称作为映射的 Windows 2000 或更高版本 id。

如果注册表项或某个适配器实例的值是相同的不同适配器类型，不可能将单个升级前的设备 ID 映射到多个 Windows 2000 或更高版本的设备 ID，而无需修改这些注册表项或值。

处理这种情况的最有效方法是按如下所示：

1.  网络迁移 DLL [ **PreUpgradeInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff562439)函数修改注册表，以便注册表包含网络适配器的每个实例的唯一值。 这些唯一值应指示适配器类型。

2.  **PreUpgradeInitialize**函数设置 NUA\_请求\_中止\_升级标志，这会导致 NetSetup 显示一条消息，提示用户重新启动 winnt32.exe 并中止升级。

3.  用户中止升级，然后重新启动 winnt32.exe。 网络迁移 DLL 现在可以使用唯一的值将映射到多个 Windows 2000 的单一升级前的设备 ID 或更高版本的设备 id。

 

 





