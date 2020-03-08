---
title: 阻止旧版文件系统筛选器驱动程序
description: 从 Windows 10 版本1607开始，管理员和驱动程序开发人员可以使用注册表设置来阻止旧式文件系统筛选器驱动程序。
ms.assetid: 90A562FB-D616-4D38-8D4F-7EFCDF9E617F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1710ab4d6187d6bb9c5453ea7bb41ca1008fe08b
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910390"
---
# <a name="blocking-legacy-file-system-filter-drivers"></a>阻止旧版文件系统筛选器驱动程序

从 Windows 10 版本1607开始，管理员和驱动程序开发人员可以使用注册表设置来阻止旧式文件系统筛选器驱动程序。 *旧式文件系统筛选器驱动程序*是直接附加到文件系统堆栈的驱动程序，不使用筛选器管理器。 本主题介绍用于阻止和取消阻止旧式文件系统筛选器驱动程序的注册表设置。 它还描述了当旧文件系统筛选器被阻止时输入到系统事件日志中的事件，以及如何检查操作系统是否有旧的文件系统驱动程序运行。

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序]((https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts))，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

## <a name="how-to-block-legacy-drivers"></a>如何阻止旧驱动程序

使用**IoBlockLegacyFsFilters**注册表项来指定系统是否阻止旧文件系统筛选器驱动程序。 当被阻止时，将阻止加载所有旧的文件系统筛选器驱动程序。 要使注册表更改生效，请重新启动系统。

必须在以下注册表路径下创建注册表项：

``` syntax
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\I/O System
```

**IoBlockLegacyFsFilters**项的有效 DWORD 值如下所示：

| **IoBlockLegacyFsFilters**值 | 说明                                                                                       |
|----------------------------------|---------------------------------------------------------------------------------------------------|
| **1**                            | 旧文件系统筛选器驱动程序被阻止加载或附加到存储卷。       |
| **0**                            | 旧文件系统筛选器驱动程序不会被阻止。 在此版本中，这是默认行为。 |

注册表编辑器中的关键如下：

![编辑 ioblocklegacyfsfilters 注册表项。](images/ioblockregkey.png)

## <a name="example-when-a-legacy-driver-is-blocked-from-loading"></a>示例：阻止加载旧驱动程序时

当阻止加载旧文件系统筛选器驱动程序时，会将一个**错误**事件记录到系统事件日志中，如下所示：

| 事件属性 | 说明 |
| -------------- | ----------- |
| 日志名称       | System      |
| 源         | Microsoft-Windows-内核-IO |
| 日期           | 12/29/2015 2:55:05 PM |
| 事件 ID       | 1205         |
| 任务类别  | 无         |
| Level          | 错误        |
| 关键字       |              |
| 用户           | CONTOSO\user |
| 计算机       | user.domain.corp.contoso.com |
| 说明    | Windows 配置为阻止旧式文件系统筛选器。 筛选器名称： \Driver\sfilter |

## <a name="how-to-check-if-legacy-drivers-are-running"></a>如何检查旧驱动程序是否正在运行

如果你不确定哪些筛选器是旧的文件系统筛选器驱动程序，或者想要确保它们未运行，则可以执行以下操作：

1. 右键单击**cmd.exe**图标，然后单击 "以**管理员身份运行**"，以打开提升的命令提示符。
2. 类型： `fltmc filters`
3. 查找旧的驱动程序，它们是**帧**值为 **&lt;旧&gt;** 的驱动程序。

在此示例中，旧的文件系统筛选器驱动程序（名为 AVLegacy 和 EncryptionLegacy）标记为 **&lt;旧&gt;** 帧值。 名为 AVMiniFilter 的文件系统驱动程序没有 **&lt;旧&gt;** 帧值，因为它是微筛选器驱动程序（它不会直接附加到文件系统堆栈并使用筛选器管理器）。

``` syntax
C:\Windows\system32>fltmc filters

Filter Name                     Num Instances    Altitude    Frame
------------------------------  -------------  ------------  -----
AVLegacy                                        389998.99   <Legacy>
EncryptionLegacy                                149998.99   <Legacy>
AVMiniFilter                           3        328000         0
```

如果你发现在阻止旧式文件系统筛选器驱动程序后遗留的驱动程序仍在运行，请确保在设置**IoBlockLegacyFsFilters**注册表项后重新启动系统。 直到重新启动后，设置才会生效。

如果系统具有旧的文件系统筛选器驱动程序，请与相应的 Isv 合作，以获取文件系统驱动程序的微筛选器版本。 有关将旧式文件系统筛选器驱动程序移植到使用筛选器管理器模型的微筛选器驱动程序的信息，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。
