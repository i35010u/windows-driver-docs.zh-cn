---
title: 一对多 ID 映射
description: 一对多 ID 映射
ms.assetid: 395d3f20-7410-496b-9ec3-1052cd731ae3
keywords:
- 映射网络组件 Id
- ID 映射 WDK netmap
- 一对多 ID 映射 WDK 网络
- preupgrade Id WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2396b4620897c1ba8074f0dd464e2a96047597d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211027"
---
# <a name="one-to-many-id-mapping"></a>一对多 ID 映射





**注意**   Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

一对多 ID 映射映射表示多个网络适配器的单个 preupgrade ID。 区分与单个 preupgrade ID 相关联的适配器的唯一方法是检查包含网络适配器实例参数值的注册表项下的值。

**OemAdapters**或**OemAsyncAdapters**节中指定一对多 ID 映射的条目具有以下格式：

*preupgrade-ID*  = *映射-方法-编号*、*节名称*

其中：

*映射-方法号* 必须为0

*节名称* 指定 netmap 文件中包含映射信息的部分

按 *节名称* 指定的 netmap 文件部分包含以下条目：

**ValueName = "**<em>Name</em>**"**

指定 NetSetup 在包含网络适配器实例参数值的注册表项下读取的值。 *名称* 标识特定网络适配器。

**ValueType =** *类型*

指定 *ValueName*的注册表值类型。 *类型* 是对应于特定注册表类型的整数。

*ValueName* = *postupgrade-ID*

*ValueName* 是 NetSetup 在包含网络适配器实例参数值的注册表项下读取的值。 *postupgrade* 是适配器的 Windows 2000 或更高版本设备 id。 应为要升级的每个适配器类型提供一个 *ValueName* 条目。 如果*ValueName*设置为关键字**ValueNotPresent** ，并且 NetSetup 未找到适配器实例的参数值，则 NetSetup 将为适配器使用与**ValueNotPresent**关联的*postuprgrade ID* 。

以下示例显示了一对多设备 ID 映射：

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

上面示例中的 **OemAdapters** 部分包含一个条目，该条目将网络适配器的 PREUPGRADE 设备 ID 标识为 DATAFIREU，并指定 netmap 文件的 **DATAFIREU** 部分包含此适配器的映射信息。

DATAFIREU 部分包含以下信息：

-   **ValueName**条目指示 NetSetup 在网络适配器实例的**Parameters**关键字下查找**BoardType**值。

-   **ValueType**项（设置为1）指定**BOARDTYPE**值为 DWORD 值。

-   剩余的每个值指定 preupgrade 设备 ID 和相应的 Windows 2000 或更高版本的 ID。 例如，DataFireIsaU 板类型的 ID 是 DATAFIRE-ISA1U。 可以指定 **ValueNotPresent** 关键字，而不是 preupgrade ID。

NetSetup 执行一对多 ID 映射，如下所示：

1.  NetSetup 读取注册表项下的指定 ValueName，其中包含网络适配器实例的参数值。

2.  NetSetup 尝试将 ValueName 与 netmap 文件的指定部分中列出的某个 ValueNames 进行匹配。 如果注册表项下未列出 ValueName，NetSetup 将尝试在 netmap 文件的指定节中查找 ValueNotPresent 关键字。

3.  如果 NetSetup 找到匹配项，它将使用与映射的 Windows 2000 或更高版本 ID 相同的 INF 文件来安装网络适配器。

如果适配器实例的注册表项或值对于不同的适配器类型是相同的，则不能将单个 preupgrade 设备 ID 映射到多个 Windows 2000 或更高版本的设备 ID，而无需首先修改这些注册表项或值。

处理此情况最有效的方法如下：

1.  网络迁移 DLL 的 [**PreUpgradeInitialize**](/previous-versions/windows/hardware/network/ff562439(v=vs.85)) 函数修改注册表，使注册表包含每个网络适配器实例的唯一值。 这些唯一值应指示适配器类型。

2.  **PreUpgradeInitialize**函数设置 NUA \_ 请求 \_ 中止 \_ 升级标志，这会导致 NetSetup 显示一条消息，提示用户重新启动 winnt32.exe 并中止升级。

3.  用户中止升级，然后重新启动 winnt32.exe。 网络迁移 DLL 现在可以使用唯一值将单个 preupgrade 设备 ID 映射到多个 Windows 2000 或更高版本的设备 ID。

 

