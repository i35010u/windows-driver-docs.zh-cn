---
title: WIA 组件
description: WIA 组件
ms.assetid: e75b8929-c16a-4c7a-9064-4fcb104bfa41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b507592ad0dccb4d10c61a1c4bd254c81093072
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714730"
---
# <a name="wia-components"></a>WIA 组件





WIA 包含多个层，这些层在用户和硬件之间调解。 用户与 WIA 应用程序交互，后者可以具有可选的用户界面。 此应用程序与 WIA 服务通信，后者将用户的请求发送到微型驱动程序。 微型驱动程序与相关的内核模式总线驱动程序通信。 最后，总线驱动程序与硬件通信。 下图说明组成 WIA 接口的软件组件。

![说明构成 wia 接口的软件组件的关系图](images/art-1.png)

### <a name="imaging-applications"></a>图像应用程序

图像处理应用程序不直接与微型驱动程序通信，而是通过 WIA API)  (WIA API 与 WIA 服务进行通信，以便从 WIA 设备访问图像和获取数据。 这些应用程序可以使用系统提供的用户界面 (UI) 或设备制造商提供的用户界面。 UI 用于选择要传输的项并设置相关的属性。 请注意，它是应用程序，而不是驱动程序，用于在关闭 UI 后传输选定项。 有关用于映像应用程序的 WIA API 的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="wia-service"></a>WIA 服务

WIA 服务是系统提供的组件，可与图像处理应用程序和 WIA 微型驱动程序进行通信。 WIA 服务是下表中列出的 COM 接口的集合，这些接口都在 Microsoft Windows SDK 文档中进行了介绍。 WIA 服务在独立于应用程序的进程中运行，但在与 WIA 微型驱动程序相同的进程中运行。 应用程序直接向 WIA 服务请求设备请求。 然后，WIA 服务将这些请求定向到相应的微型驱动程序，通过 WIA 设备驱动程序接口 (WIA DDI) 。 下表列出了 WIA 应用程序可以实现的 Api。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA API</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IEnumWIA_DEV_CAPS</strong></p></td>
<td><p>枚举 WIA 硬件设备的功能。 设备功能包括设备支持的命令和事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWIA_DEV_INFO</strong></p></td>
<td><p>枚举 WIA 硬件设备及其属性。 设备信息属性介绍 WIA 硬件设备的安装和配置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IEnumWIA_FORMAT_INFO</strong></p></td>
<td><p>枚举设备的格式和媒体类型信息。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWiaItem</strong></p></td>
<td><p>枚举树的当前文件夹中的 <strong>IWiaItem</strong> 对象。 WIA 运行时系统将应用程序的每个 WIA 硬件设备表示为 <strong>IWiaItem</strong> 对象的层次结构树。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDataCallback</strong></p></td>
<td><p>提供从 WIA 硬件设备到应用程序的数据传输过程中的应用程序回调机制。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaDataTransfer</strong></p></td>
<td><p>支持使用 "共享内存" 窗口将数据从设备对象传输到应用程序，并在封送过程中消除不必要的数据复制。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDevMgr</strong></p></td>
<td><p>由应用程序用来创建和管理映像获取设备。 它们还使用它来注册以接收设备事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaEventCallback</strong></p></td>
<td><p>由应用程序用来接收 WIA 硬件设备事件的通知。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaItem</strong></p></td>
<td><p>使应用程序能够查询设备的功能。 <strong>IWiaItem</strong> 还提供对数据传输接口和项属性的访问。 此外，此接口还提供了用于使应用程序能够控制设备的方法。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaPropertyStorage</strong></p></td>
<td><p>提供对 <strong>IWiaItem</strong> 对象属性的信息的访问。</p></td>
</tr>
</tbody>
</table>

 

### <a name="wia-driver-services-library"></a>WIA 驱动程序服务库

[Wia 驱动程序服务库](wia-driver-services-library.md)是系统提供的组件，它为 WIA 微型驱动程序提供 helper 函数。 微型驱动程序可以调用 helper 函数来执行任务，如下所示：

-   初始化 [WIA 驱动程序项树](wia-driver-item-tree.md)。

-   读取、写入和验证设备属性。

-   传输数据。

或者，微型驱动程序可以执行此类任务本身。 通过使用 helper 函数，你可以减少开发时间和 WIA 微型驱动程序的大小，还可以灵活地开发单个解决方案。

### <a name="wia-utility-library"></a>WIA 实用程序库

[WIA 实用工具库](wia-utility-library.md)包含调试函数的集合 ( **wiauDbg * * * Xxx*) 、常规实用工具 helper 函数的集合和三个类： **CWiauDbgFn**类、 **CWiauFormatConverter**类和**CWiauPropertyList**类。

### <a name="wia-minidrivers"></a>WIA 微型驱动程序

[Wia 微型驱动程序](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv) 是由供应商提供的用户模式组件，可将 WIA 属性更改和命令定向到图像设备。 微型驱动程序实现 WIA DDI，WIA 服务调用它来与微型驱动程序进行通信。

WIA 微型驱动程序向内核模式静止映像驱动程序提供特定于设备的用户模式接口，该驱动程序通过驱动程序（如 USB 驱动程序）驱动图像设备。 微型驱动程序通过调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**和 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) Microsoft Win32 (函数（Microsoft Windows SDK 文档) 中所述）来与内核模式驱动程序通信。

图像应用程序不能直接调用 WIA 微型驱动程序。 只有 WIA 服务可以直接调用该驱动程序。

### <a name="kernel-io-drivers"></a>内核 i/o 驱动程序

内核模式静止映像驱动程序是系统提供的或由 IHV 提供的组件，这些组件打包用于传递到仍图像设备并从静止图像设备传输的数据。 内核模式的静止映像驱动程序是特定于总线的。

Microsoft 为 USB、SCSI、串行和 IEEE 1394 总线提供 Microsoft Windows 驱动模型 (WDM) 的内核模式静止映像驱动程序。 有关这些驱动程序的详细信息，请参阅 [访问静止图像设备的内核模式驱动程序](accessing-kernel-mode-drivers-for-still-image-devices.md)。

仅当供应商的图像处理设备与 Microsoft 提供的内核模式 i/o 驱动程序不兼容时，供应商才必须提供该驱动程序的内核模式。

**注意**   在 Windows XP 和更高版本中，可以从驱动程序中检索版本信息。 [**Wia \_ dip \_ WIA \_ 版本**](./wia-dip-wia-version.md)属性包含 WIA 版本， [**wia \_ dip \_ 驱动程序 \_ 版本**](./wia-dip-driver-version.md)属性包含驱动程序 DLL 版本。 WIA 服务创建并维护这些属性;加载驱动程序时，WIA 服务会自动添加它们。 Windows Me 不包含这些属性。

 

 

