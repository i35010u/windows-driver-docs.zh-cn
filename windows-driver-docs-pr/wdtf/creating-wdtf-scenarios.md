---
title: 创建 WDTF 方案
description: 使用 WDTF 方案中，你构建使用 WDTF framework 专注于设备的自动和自定义测试方案。
ms.assetid: f9e3de20-28be-40c6-802c-f4637b3f6c20
keywords:
- Windows 设备测试框架 WDK 脚本
- WDTF WDK 脚本
- 脚本 WDK WDTF
- 测试脚本 WDK WDTF
- 虚拟设备 WDK WDTF
- 删除的设备 WDK WDTF
- 热插拔设备 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6f6331d52f5f49e220739ab9c53bfcea569bb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338978"
---
# <a name="creating-wdtf-scenarios"></a>创建 WDTF 方案


可以通过创建的实例启动基于 WDTF 的方案[ **IWDTF2** ](https://msdn.microsoft.com/library/windows/hardware/ff539628)聚合接口，其中包含[ **DeviceDepot** ](https://msdn.microsoft.com/library/windows/hardware/hh406304)并[ **SystemDepot** ](https://msdn.microsoft.com/library/windows/hardware/hh406309)属性。

若要收集一个或多个目标对象，请使用[ **IWDTFDeviceDepot2** ](https://msdn.microsoft.com/library/windows/hardware/hh406391)接口，并使用**查询**方法使用[简单数据评估语言](simple-data-evaluation-language-overview.md) (SDEL)。

脚本还可能会通过检查特定目标[ **IWDTFTarget2::Eval** ](https://msdn.microsoft.com/library/windows/hardware/hh439396)方法。 选择目标后，它们通过使用来控制[一个或多个操作接口](controlling-targets.md)。

在开始开发 WDTF 方案之前，必须安装 WDTF。 请参阅[WDTF 快速启动](wdtf-quick-start-.md)有关详细信息。

本主题中的以下部分介绍如何创建基本 WDTF 方案。

### <a name="simple-wdtf-scenario"></a>简单 WDTF 方案

下面的 VBScript 代码示例 (WDTF\_Sample1.vbs) 显示了使用 WDTF 来启用和禁用每个非接触的虚拟设备的简化的方案。 一个*非接触的虚拟设备*是实际存在的任何设备。 有关完整示例，请参阅[示例 WDTF 方案](sample-wdtf-scenarios.md)。

```cpp
Set WDTF = WScript.CreateObject("WDTF.WDTF")
For Each Device In WDTF.DeviceDepot.Query("IsPhantom=false AND IsDisableable")
    On Error Resume Next
    Set DevMan = Device.GetInterface("DeviceManagement")
    If err <> 0 Then
 DevMan.Disable()
 DevMan.Enable()
    End If
Next
```

可以通过运行运行这种情况下**CScript.exe WDTF\_Sample1.vbs**。

### <a name="storing-target-information-by-using-context"></a>将目标信息存储使用的上下文

某些编程语言，如 VBScript、 不方便地管理对象的引用。 为了简化这种管理 WDTF 中的，每个目标提供了[**上下文**](https://msdn.microsoft.com/library/windows/hardware/hh439393)属性，您可以使用存储任意键/值对，其中包括对活动对象的引用。 此属性是用于存储操作接口，以便以后使用它们特别有用。 以下 VBScript 代码示例存储[ **IWDTFSimpleIOStressAction2** ](https://msdn.microsoft.com/library/windows/hardware/hh451157)中的已命名操作**上下文**项。

```cpp
deviceObj.Context("IWDTFSimpleIOStressAction2") = SimpleIOObj
```

你的方案更高版本，可以停止、 暂停或重新启动[ **IWDTFSimpleIOStressAction2** ](https://msdn.microsoft.com/library/windows/hardware/hh451157)通过访问通过接口[**上下文**](https://msdn.microsoft.com/library/windows/hardware/hh439393)同样，为以下代码示例所示。

```cpp
Device.Context("IWDTFSimpleIOStressAction2").Stop
```

### <a name="detecting-phantom-devices"></a>检测虚拟设备

虚拟设备是在过去以物理方式在计算机安装的设备，但当前不存在。 例如，虚拟设备可能已被拔出 USB 鼠标。 若要加快和简化重新安装设备插入到已打开，或删除设备的计算机，Windows 操作系统保留安装的设备驱动程序，但将标记作为接触的虚拟设备。

设备类型目标包括**IsPhantom**属性 (和**IsAttached**属性，它等效于**IsPhantom**= false)，它指定的物理硬件存在。 下面的 VBScript 代码示例列出了的计算机中物理上存在的所有设备的集合。

```cpp
Set NonPhantomDevices = WDTF.DeviceDepot.Query ("IsAttached")
```

有关更多属性关键字，请参阅[SDEL 令牌](https://msdn.microsoft.com/library/windows/hardware/ff539571)。

 

 




