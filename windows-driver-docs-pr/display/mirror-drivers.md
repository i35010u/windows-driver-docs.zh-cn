---
title: 镜像驱动程序
description: 镜像驱动程序
ms.assetid: 7231375a-969b-4c55-83d4-96ba5caade20
keywords:
- 显示驱动程序 WDK Windows 2000 中，镜像驱动程序
- 镜像驱动程序 WDK Windows 2000 显示
- 虚拟桌面的 WDK Windows 2000 时，显示
- 镜像 WDK Windows 2000 显示全局桌面
- GDI 虚拟桌面 WDK Windows 2000 显示
- 镜像 WDK Windows 2000 显示的虚拟设备
- 微型端口驱动程序 WDK Windows 2000 中，镜像驱动程序
- 辅助技术和镜像驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c977d484fa9f698afb2db77400efd5a2b821a740
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352427"
---
# <a name="mirror-drivers"></a>镜像驱动程序


## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [远程显示器驱动程序](remote-display-drivers.md)
-   [视频端口 DDI 支持](video-port-ddi-support.md)
-   [镜像驱动程序 INF 文件](mirror-driver-inf-file.md)
-   [镜像驱动程序安装](mirror-driver-installation.md)

## <a name="span-idmirrordriversinwindows8spanspan-idmirrordriversinwindows8spanspan-idmirrordriversinwindows8spanmirror-drivers-in-windows8"></a><span id="Mirror_drivers_in_Windows_8"></span><span id="mirror_drivers_in_windows_8"></span><span id="MIRROR_DRIVERS_IN_WINDOWS_8"></span>在 Windows 8 中的镜像驱动程序


从 Windows 8 开始，镜像驱动程序不会安装在系统上。 在本部分中所述的镜像驱动程序将安装并仅在早期版本的 Windows 上运行。

但是，特殊的 GDI 辅助功能驱动程序模型是从 Windows 8 开始对开发人员想要提供镜像中的驱动程序功能提供[*辅助技术*](https://go.microsoft.com/fwlink/p/?linkid=248209)具有的客户残障人士或障碍。 若要了解有关此特殊的驱动程序模型的详细信息，请联系<acc_driver@microsoft.com>。

一个*远程显示器驱动程序*基于镜像驱动程序体系结构的模型还可以从 Windows 8 开始运行。 有关详细信息，请参阅[远程显示器驱动程序](remote-display-drivers.md)。

## <a name="span-idddkmirrordriversggspanspan-idddkmirrordriversggspanmirror-driver-description"></a><span id="ddk_mirror_drivers_gg"></span><span id="DDK_MIRROR_DRIVERS_GG"></span>镜像驱动程序的描述


一个*镜像驱动程序*是反映一个或多个其他物理显示设备的绘制操作的虚拟设备的显示驱动程序。 它实现和行为非常类似于任何其他显示器驱动程序;但是，其配对微型端口驱动程序很小相比典型的微型端口驱动程序。 请参阅[视频微型端口驱动程序 （Windows 2000 模式） 中的镜像驱动程序支持](mirror-driver-support-in-video-miniport-drivers--windows-2000-model-.md)镜像系统中的微型端口驱动程序有关的详细信息。 通过 Windows 7 版本 (版本 7600) Windows Driver Kit (WDK) 包含其中包括三个目录中的组件源包含的文件的一个示例镜像驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">包含源代码文件</th>
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
<td align="left"><p>用户模式的服务。 此外包含<em>mirror.inf。</em></p></td>
</tr>
</tbody>
</table>

 

支持 GDI*虚拟桌面*并提供的功能来复制虚拟机镜像设备上的部分。 GDI 作为物理显示器驱动程序层之上的图形层来实现虚拟桌面。 在此虚拟桌面空间; 启动所有绘制操作GDI 剪辑并将它们呈现在虚拟桌面中存在适当的物理显示设备上。

镜像设备都可以指定任意*剪辑区域*虚拟桌面，在其中一个跨多个物理显示器的设备。 GDI 然后将镜像设备发送该驱动程序的剪辑区域相交的所有绘制操作。 镜像设备可以设置与特定的物理设备; 完全匹配的剪辑区域因此，它可以有效地反映该设备。

**请注意**  镜像驱动程序的剪辑区域必须在 Windows 2000 及更高版本，包括主显示设备。

 

**请注意**  镜像驱动程序加载时，桌面 Windows 管理器 (DWM) 在 Windows Vista 和更高版本，已关闭。

 

*镜像*驱动程序的代码示例演示如何实现镜像驱动程序。 有关详细信息，将帮助您了解该示例：

-   使用示例 INF 文件*mirror.inf*，作为模板。 请参阅[镜像驱动程序 INF 文件](mirror-driver-inf-file.md)有关详细信息。

-   请参阅*mirror.exe*应用程序中，该示例演示了如何镜像驱动程序附加到虚拟桌面。 请参阅[镜像驱动程序安装](mirror-driver-installation.md)有关详细信息。

-   请参阅 Windows SDK 文档，以了解有关使用 Win32 **EnumDisplayDevices**函数。 使用此函数来确定 **\\ \\。\\显示\#** 与镜像的显示设备相关联的名称。 此数目是所需更改镜像设备的设置。 对于多个实例， **\#** 是不同数量的每个实例; 因此必须通过循环的可用的显示设备确定此数字。

**若要将镜像的设备附加到全局桌面**

1.  添加 REG\_DWORD 注册表项**Attach.ToDesktop**驱动程序的服务密钥。

2.  将此密钥条目设置为 1 （一）。

若要禁用镜像驱动程序，请将此条目设置为 0 （零）。

正如前面提到的该驱动程序安装，并在驻留设备层之上绘制层运行。 由于镜像驱动程序的坐标空间是桌面坐标空间，它可以跨多个设备。 如果镜像驱动程序旨在镜像主显示器，其显示坐标应与主显示器的桌面坐标一致。

-   镜像驱动程序安装后，它将调用所有相交驱动程序的显示区域的呈现操作。 上[多监视器系统](multiple-monitor-support-in-the-display-driver.md)，这可能包括所有绘制操作，如果镜像驱动程序与重叠只有主显示器设备。

-   建议用户模式服务用于维护镜像驱动程序的设置。 此应用程序可以确保在启动时正确加载驱动程序，它可以相应地更改到桌面通过响应获取 WM 通过显示更改的通知\_DISPLAYCHANGE 消息。

-   GDI 调用任何 2D 图形 DDI 相交驱动程序的边框的绘制操作镜像驱动程序。 请注意 GDI 不在图面是设备格式位图; 是否执行边界矩形检查也就是说，如果[ **SURFOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff569901)具有**iType**的 STYPE\_DEVBITMAP。

-   与往常一样，镜像驱动程序必须实现无需使用全局变量。 所有状态必须都存在于*PDEV*该特定驱动程序。 将调用 GDI [ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)为创建的微型端口驱动程序的每个硬件设备扩展。

-   镜像驱动程序应支持 DirectDraw。

-   镜像驱动程序必须设置 GCAPS\_分层标志**TRUE**中**flGraphicsCaps**隶属[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。

-   可访问性镜像驱动程序必须设置 GCAPS2\_EXCLUDELAYERED 和 GCAPS2\_INCLUDEAPIBITMAPS 到标志**TRUE**中**flGraphicsCaps2** 成员[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。

-   镜像驱动程序 （可选） 可以通过实现来支持画笔揭示[ **DrvRealizeBrush**](https://msdn.microsoft.com/library/windows/hardware/ff556273)。

GDI 使相同的驱动程序的单个和多监视器系统上运行。 多监视器系统中的驱动程序只需要跟踪全局桌面中的位置。 GDI 提供此位置向驱动程序只要 Win32 **ChangeDisplaySettings**调用发生，例如当用户动态更改监视器的位置在 desktop 中通过使用控制面板中的显示计划。 GDI 更新**dmPosition**的成员[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构相应地，发生此类更改时。 驱动程序可以通过实现来接收此类更改的通知[ **DrvNotify**](https://msdn.microsoft.com/library/windows/hardware/ff556252)。 请参阅[镜像驱动程序安装](mirror-driver-installation.md)有关详细信息。

**请注意**  镜像驱动程序不需要呈现完全适合像素的准确性时，此类准确度在客户端上的呈现可能比较困难。 例如，适配器/监视器接收镜像的映像不需要呈现[网格相交量化](cosmetic-lines.md)(GIQ) 线条和多边形填充适配器/监视器正在镜像相同的精度。

 

 

 





