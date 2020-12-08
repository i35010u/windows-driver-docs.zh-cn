---
title: 创建 WDTF 方案
description: 使用 WDTF 方案，你可以使用 WDTF 框架构建以设备为中心的自动化和自定义测试方案。
keywords:
- Windows 设备测试框架 WDK，脚本
- WDTF WDK，脚本
- 脚本 WDK WDTF
- 测试脚本 WDK WDTF
- 虚拟设备 WDK WDTF
- 删除的设备 WDK WDTF
- 热更换设备 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3aa9771c300432f8b86f6f4bbb125aa987f7e30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785397"
---
# <a name="creating-wdtf-scenarios"></a>创建 WDTF 方案


可以通过创建 [**IWDTF2**](/windows-hardware/drivers/ddi/index) 聚合接口的实例（其中包含 [**DeviceDepot**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_devicedepot) 和 [**SYSTEMDEPOT**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_systemdepot) 属性）开始基于 WDTF 的方案。

若要收集一个或多个目标对象，请使用 [**IWDTFDeviceDepot2**](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfdevicedepot2) 接口，并将 **Query** 方法与 [简单的数据计算语言](simple-data-evaluation-language-overview.md) 一起使用 (SDEL) 。

脚本还可以通过使用 [**IWDTFTarget2：： Eval**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval) 方法来检查特定目标。 选择目标后，使用 [一个或多个操作接口](controlling-targets.md)对其进行控制。

在开始开发 WDTF 方案之前，必须安装 WDTF。 有关详细信息，请参阅 [WDTF 快速入门](wdtf-quick-start-.md) 。

本主题中的以下部分介绍如何创建基本的 WDTF 方案。

### <a name="simple-wdtf-scenario"></a>简单的 WDTF 方案

以下 VBScript 代码示例 (WDTF \_Sample1.vbs) 显示了一个简化的方案，该方案使用 WDTF 来启用和禁用每个非虚拟设备。 *非虚拟设备* 是任何物理上存在的设备。 有关完整示例，请参阅 [示例 WDTF 方案](sample-wdtf-scenarios.md)。

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

可以通过运行 **CScript.exe WDTF \_Sample1.vbs** 运行此方案。

### <a name="storing-target-information-by-using-context"></a>使用上下文存储目标信息

某些编程语言（例如 VBScript）不容易管理对象引用。 为了简化 WDTF 中的这一管理，每个目标都提供一个 [**上下文**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-put_context) 属性，可用于存储任意键/值对（包括对活动对象的引用）。 此属性特别适用于存储操作接口，以便以后可以使用。 以下 VBScript 代码示例在命名 **上下文** 项中存储 [**IWDTFSimpleIOStressAction2**](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)操作。

```cpp
deviceObj.Context("IWDTFSimpleIOStressAction2") = SimpleIOObj
```

稍后，你的方案可以通过 [**上下文**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-put_context)再次访问来停止、暂停或重新启动 [**IWDTFSimpleIOStressAction2**](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)接口，如下面的代码示例所示。

```cpp
Device.Context("IWDTFSimpleIOStressAction2").Stop
```

### <a name="detecting-phantom-devices"></a>检测虚拟设备

虚拟设备是指过去在计算机上实际安装但当前不存在的设备。 例如，虚拟设备可能是已拔出的 USB 鼠标。 为了加速和简化重新安装插入到已打开或已删除设备的计算机上的设备，Windows 操作系统将保留安装的设备驱动程序，但将设备标记为虚拟设备。

设备类型目标包括 **IsPhantom** 属性 (和 **IsAttached** 属性，该属性等效于指定硬件物理存在的 **IsPhantom**= false) 。 下面的 VBScript 代码示例列出了计算机中物理上存在的所有设备的集合。

```cpp
Set NonPhantomDevices = WDTF.DeviceDepot.Query ("IsAttached")
```

有关更多特性关键字，请参阅 [SDEL 标记](/windows-hardware/drivers/ddi/index)。

 

