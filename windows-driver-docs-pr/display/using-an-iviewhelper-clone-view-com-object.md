---
title: 使用 IViewHelper 克隆视图 COM 对象
description: 使用 IViewHelper 克隆视图 COM 对象
ms.assetid: 2f264c5d-0e12-4116-9561-16dce99ce1fe
keywords:
- 有关 IViewHelper TMM WDK 显示器
- 监视配置 WDK 显示有关 IViewHelper
- 监视器配置 WDK 显示区域，检测新的监视器
- 监视配置 WDK 显示，保存
- 有关 IViewHelper 视频存在网络 WDK 显示
- 有关 IViewHelper VidPN WDK 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5270208041af24fbf168805a311d1f2f46129838
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534814"
---
# <a name="using-an-iviewhelper-clone-view-com-object"></a>使用 IViewHelper 克隆视图 COM 对象


TMM 将使用硬件供应商的克隆视图的方法[IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)在新的监视器和持久化的监视器配置中的 COM 接口对象。 在持久化的监视器配置中，TMM 将显示数据 （即，显示模式和拓扑的数据） 还原到监视器。 TMM 可以将此显示的数据传递给用户模式显示驱动程序通过[ **IViewHelper::SetConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff568176)方法，使驱动程序可以修改或在其他显示数据 （例如，gamma 或电视折叠设置）。

中的错误[视频存在网络 (VidPN)](multiple-monitors-and-video-present-networks.md)通过的方法返回[IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)。 因此，如果 TMM 适用的不正确的拓扑，VidPN 失败和失败结果传递回调用的函数。 将目标映射到两个源或使用 VidPN 无法识别的目标或源标识符是拓扑的不正确的示例。

确定 TMM [IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)通过 COM 接口对象**UserModeDriverGUID**字符串注册表值。 硬件供应商应添加此注册表值键**DeviceKey**显示的成员\_设备结构指定。 调用 Win32 **EnumDisplayDevices**函数返回此注册表项信息中显示\_设备的*lpDisplayDevice*参数指向。 如果多个**DeviceKey**名称存在，此值应显示的每个这些密钥。 以下是设备密钥的示例和**UserModeDriverGUID**字符串注册表值：

```registry
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Video\{7661971C-A9BD-48B5-ACBC-298A8826535D}\0000]
"UserModeDriverGUID"="{YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY}"
```

若要加载的 com [IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164) COM 接口的对象，应作为进程 （进程内） 处理程序，注册的 COM 对象和线程处理模型应同时。 已注册的 GUID 应与中的 GUID 匹配**UserModeDriverGUID**。 有关这两个线程处理模型属性的信息，请参阅 Microsoft Windows SDK 文档。

您应该仅复制并注册正确编译的版本[IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)系统目录中的 COM 接口对象的 Dll。 也就是说，您应该仅复制并注册 64 位**IViewHelper**对 64 位操作系统和 32 位 DLL **IViewHelper** 32 位操作系统的 DLL。 两个 DLL 二进制文件不应同时存在于同一台计算机上。 如果两个二进制文件均同时存在于同一台计算机，甚至与 Windows on Windows (WOW) TMM 将无法正常运行。

 

 





