---
title: 镜像驱动程序
description: 镜像驱动程序
ms.assetid: 7231375a-969b-4c55-83d4-96ba5caade20
keywords:
- 显示驱动程序 WDK Windows 2000，镜像驱动程序
- 镜像驱动程序 WDK Windows 2000 显示
- 虚拟桌面 WDK Windows 2000 显示
- 全局桌面镜像 WDK Windows 2000 显示
- GDI 虚拟桌面 WDK Windows 2000 显示
- 虚拟设备镜像 WDK Windows 2000 显示
- 视频微型端口驱动程序 WDK Windows 2000，镜像驱动程序
- 辅助技术和镜像驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 364e9126fb2e02e1d345d27adb48ede352bff7ae
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066030"
---
# <a name="mirror-drivers"></a>镜像驱动程序

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [远程显示驱动程序](remote-display-drivers.md)
-   [视频端口 DDI 支持](video-port-ddi-support.md)
-   [镜像驱动程序 INF 文件](mirror-driver-inf-file.md)
-   [镜像驱动程序安装](mirror-driver-installation.md)

## <a name="mirror-drivers-in-windows8-and-above"></a>Windows 8 及更高版本中的镜像驱动程序

从 Windows 8 开始，镜像驱动程序将不会安装在系统上。 本节中所述的镜像驱动程序将仅在早期版本的 Windows 上安装和运行。

但是，从 Windows 8 开始，可以使用一种特殊的 GDI 辅助功能驱动程序模型，开发人员需要为残障或障碍客户提供 [*辅助技术*](https://go.microsoft.com/fwlink/p/?linkid=248209) 中的镜像驱动程序功能。 若要了解有关此特殊驱动程序模型的详细信息，请联系 <acc_driver@microsoft.com> 。

基于镜像驱动程序体系结构的 *远程显示驱动程序* 模型也可以从 windows 8 开始运行，但在 windows 10 版本2004中已删除。 有关详细信息，请参阅 [远程显示驱动程序](remote-display-drivers.md)。

> [!NOTE]
>
> 在 Windows 10 中，不再建议使用 GDI 辅助功能驱动程序用于新产品，Microsoft 将在将来的操作系统版本中删除支持。 Windows 10 版本2004中已删除对 GDI 远程显示驱动程序的支持。 但是，仍然可以通过构建自定义 [远程协议提供](/windows/win32/termserv/creating-a-custom-remote-protocol) 程序和 [间接显示驱动](indirect-display-driver-model-overview.md)程序来创建远程显示解决方案。

## <a name="span-idddk_mirror_drivers_ggspanspan-idddk_mirror_drivers_ggspanmirror-driver-description"></a><span id="ddk_mirror_drivers_gg"></span><span id="DDK_MIRROR_DRIVERS_GG"></span>镜像驱动程序描述


*镜像驱动程序*是虚拟设备的显示驱动程序，该驱动程序对一个或多个附加物理显示设备的绘图操作进行镜像。 它的实现与任何其他显示驱动程序的行为非常相似;但是，与典型的微型端口驱动程序相比，其配对的视频微型端口驱动程序是最少的。 有关镜像系统中的微型端口驱动程序的详细信息，请参阅 [ (Windows 2000 型号的视频微型端口驱动程序中的镜像驱动程序支持) ](mirror-driver-support-in-video-miniport-drivers--windows-2000-model-.md) 。 Windows 驱动程序工具包 (WDK) 通过 Windows 7 edition (版本 7600) 包含包含在三个目录中的组件源文件的示例镜像驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">包含的源文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>\src\video\displays\mirror\disp</p></td>
<td align="left"><p>镜像驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>\src\video\miniport\mirror\mini</p></td>
<td align="left"><p>微型端口驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>\src\video\displays\mirror\app</p></td>
<td align="left"><p>用户模式服务。 还包含 <em>镜像 .inf。</em></p></td>
</tr>
</tbody>
</table>

GDI 支持 *虚拟桌面* ，并提供在镜像设备上复制部分虚拟桌面的功能。 GDI 将虚拟桌面作为物理显示器驱动程序层之上的图形层来实现。 所有绘图操作都在此虚拟桌面空间中启动;GDI 剪辑，并将其呈现在虚拟机中存在的相应物理显示设备上。

镜像设备可以指定虚拟桌面中的任意剪辑区域，其中包括跨多个物理显示设备的 *剪辑区域* 。 然后，GDI 将发送镜像设备与该驱动程序的剪辑区域相交的所有绘图操作。 镜像设备可以设置与特定物理设备完全匹配的剪辑区域;因此，它可以有效地镜像该设备。

> [!NOTE]
>
> 在 Windows 2000 和更高版本中，镜像驱动程序的剪辑区域必须包括主显示设备。
>
> 在 Windows Vista 和更高版本中，当加载镜像驱动程序时，桌面 Windows 管理器 (DWM) 将关闭。

*镜像*驱动程序代码示例说明了如何实现镜像驱动程序。 有关有助于了解示例的详细信息，请执行以下操作：

-   使用示例 INF 文件作为模板 *。* 有关详细信息，请参阅 [镜像驱动程序 INF 文件](mirror-driver-inf-file.md) 。

-   请参阅 *mirror.exe* 应用程序，该应用程序演示镜像驱动程序如何附加到虚拟桌面。 有关详细信息，请参阅 [镜像驱动程序安装](mirror-driver-installation.md) 。

-   有关使用 Win32 **EnumDisplayDevices** 函数的信息，请参阅 Windows SDK 文档。 使用此函数可确定** \\ \\ 。 \\显示 \# **与镜像显示设备关联的名称。 更改镜像设备的设置需要此数字。 对于多个实例， **\#** 每个实例都是不同的编号; 因此，必须通过循环访问可用的显示设备来确定此数字。

**将镜像设备附加到全局桌面**

1.  将 REG \_ DWORD 注册表项 **ToDesktop** 添加到驱动程序的服务密钥。

2.  将此项的条目设置为 1 (一个) 。

若要禁用镜像驱动程序，请将此项设置为 0 (零) 。

如前所述，驱动程序已安装并在位于设备层的绘图层中运行。 由于镜像驱动程序的坐标空间是桌面坐标空间，因此它可以跨多个设备。 如果镜像驱动程序用于镜像主显示器，则其显示坐标应与主显示器的桌面坐标一致。

-   镜像驱动程序安装完成后，将为与该驱动程序的显示区域相交的所有呈现操作调用它。 在 [多监视器系统](multiple-monitor-support-in-the-display-driver.md)中，如果镜像驱动程序仅与主显示设备重叠，则这可能不包括所有绘图操作。

-   建议使用用户模式服务来维护镜像驱动程序的设置。 此应用程序可确保在启动时正确加载该驱动程序，并且它可以通过使用 WM DISPLAYCHANGE 消息获取显示更改通知，对桌面的更改做出适当的响应 \_ 。

-   GDI 为与驱动程序的边框相交的任何2D 图形 DDI 绘图操作调用镜像驱动程序。 请注意，如果图面为设备格式位图，则 GDI 不会执行边框检查;也就是说，如果 [**SURFOBJ**](/windows/desktop/api/winddi/ns-winddi-_surfobj) 具有 **iType** 的 s \_ DEVBITMAP。

-   与往常一样，必须在不使用全局变量的情况下实现镜像驱动程序。 该特定驱动程序的 *PDEV* 中必须存在所有状态。 GDI 将为视频微型端口驱动程序创建的每个硬件设备扩展调用 [**DrvEnablePDEV**](/windows/desktop/api/winddi/nf-winddi-drvenablepdev) 。

-   镜像驱动程序不应支持 DirectDraw。

-   镜像驱动程序必须 \_ 在[**lnk-devinfo**](/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构的**FLGRAPHICSCAPS**成员中将 GCAPS 分层标志设置为**TRUE** 。

-   辅助功能镜像驱动程序必须 \_ \_ 在[**FlGraphicsCaps2**](/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构的**Lnk-devinfo**成员中将 GCAPS2 EXCLUDELAYERED 和 GCAPS2 INCLUDEAPIBITMAPS 标志设置为**TRUE** 。

-   镜像驱动程序可以通过实现 [**DrvRealizeBrush**](/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)（可选）支持画笔实现。

GDI 允许在单个和多个监视器系统上同时运行同一驱动程序。 多监视器系统中的驱动程序只需跟踪其在全局桌面中的位置。 在发生 Win32 **ChangeDisplaySettings** 调用时，GDI 为驱动程序提供了此位置，例如，当用户使用控制面板中的 "显示" 程序动态更改监视器在桌面上的位置时。 当发生这种更改时，GDI 会相应地更新[**DEVMODEW**](/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构的**dmPosition**成员。 驱动程序可以通过实现 [**DrvNotify**](/windows/desktop/api/winddi/nf-winddi-drvnotify)来接收此类更改的通知。 有关详细信息，请参阅 [镜像驱动程序安装](mirror-driver-installation.md) 。

> [!NOTE]
>
> 当在客户端上呈现时，镜像驱动程序无需像素精确的准确性，因此可能很难。 例如，不需要接收镜像映像的适配器/监视器来呈现 [网格交集量化](cosmetic-lines.md) (GIQ) 直线绘图和多边形填充与正在镜像的适配器/监视器的精度相同。