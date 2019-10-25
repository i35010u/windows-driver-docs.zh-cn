---
title: 使用 IViewHelper Clone-View COM 对象
description: 使用 IViewHelper Clone-View COM 对象
ms.assetid: 2f264c5d-0e12-4116-9561-16dce99ce1fe
keywords:
- TMM WDK 显示，关于 IViewHelper
- 监视器配置 WDK 显示，关于 IViewHelper
- 监视配置 WDK 显示，检测新监视器
- 监视配置 WDK 显示，持久化
- 视频显示网络 WDK 显示，关于 IViewHelper
- VidPN WDK 显示，关于 IViewHelper
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9491779601946a4df53684b2145e3757a0e82b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829289"
---
# <a name="using-an-iviewhelper-clone-view-com-object"></a>使用 IViewHelper Clone-View COM 对象


TMM 将使用新监视器中的硬件供应商克隆查看[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM 接口对象的方法，并保留监视器配置。 在持久化监视器配置中，TMM 会将显示数据（即显示模式和拓扑数据）还原为监视器。 TMM 可以通过[**IViewHelper：： SetConfiguration**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568176(v=vs.85))方法将此显示数据传递给用户模式显示驱动程序，以便驱动程序可以修改或折叠其他显示数据（例如，伽玛或电视设置）。

来自[视频提供网络（VidPN）](multiple-monitors-and-video-present-networks.md)的错误是通过[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的方法返回的。 因此，如果 TMM 应用不正确的拓扑，则 VidPN 将失败，并且失败结果会传递回调用函数。 将目标映射到两个源或使用 VidPN 无法识别的目标或源标识符就是不正确的拓扑示例。

TMM 通过**UserModeDriverGUID** string 注册表值确定[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM 接口对象。 硬件供应商应该将此值添加到\_设备结构的显示的**DeviceKey**成员所指定的注册表项下。 对 Win32 **EnumDisplayDevices**函数的调用会将此注册表项信息返回到*lpDisplayDevice*参数指向的\_设备显示。 如果存在多个**DeviceKey**名称，则此值应显示在每个键下。 下面是设备密钥和**UserModeDriverGUID**字符串注册表值的示例：

```registry
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Video\{7661971C-A9BD-48B5-ACBC-298A8826535D}\0000]
"UserModeDriverGUID"="{YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY}"
```

要使 COM 加载[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) com 接口对象，应将 COM 对象注册为进程内（进程内）处理程序，并且线程模型应同时为两者。 已注册的 GUID 应该与**UserModeDriverGUID**中的 guid 匹配。 有关这两个线程模型属性的信息，请参阅 Microsoft Windows SDK 文档。

只应复制并注册系统目录中的[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM 接口对象 dll 的正确编译版本。 也就是说，只应为64位操作系统复制和注册64位**IViewHelper** dll，为32位操作系统复制并注册32位**IViewHelper** dll。 两个 DLL 二进制文件不应同时出现在同一台计算机上。 如果两个二进制文件同时存在于同一台计算机上（即使 windows on Windows （WOW）），则 TMM 将无法正常运行。

 

 





