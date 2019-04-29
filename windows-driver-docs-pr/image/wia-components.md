---
title: WIA 组件
description: WIA 组件
ms.assetid: e75b8929-c16a-4c7a-9064-4fcb104bfa41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44b07e5da2591790aefa18a8665e5c1766a9da75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366999"
---
# <a name="wia-components"></a>WIA 组件





WIA 由用户与硬件之间进行调解的多个层组成。 在用户与 WIA 应用程序，可以具有可选的用户界面交互。 此应用程序与 WIA 服务，可将用户的请求发送到微型驱动程序进行通信。 微型驱动程序与相关的内核模式总线驱动程序进行通信。 最后，总线驱动程序与硬件进行通信。 下图说明了组成 WIA 接口的软件组件。

![说明组成 wia 接口的软件组件的关系图](images/art-1.png)

### <a name="imaging-applications"></a>图像处理应用程序

图像处理应用程序不能直接与微型驱动程序，但它们与通过 WIA 应用程序编程接口 (WIA API) 来访问图像，并获得 WIA 的设备中的数据的 WIA 服务通信。 这些应用程序可以使用系统提供用户界面 (UI) 或设备的制造商提供的其中一个。 若要选择的传输项目以及设置相关属性，使用 UI。 请注意，它是应用程序不是驱动程序，关闭 UI 后传输所选的项目。 有关图像处理应用程序 WIA API 的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="wia-service"></a>WIA 服务

WIA 服务是与图像处理应用程序和 WIA 微型驱动程序进行通信的系统提供的组件。 WIA 服务是下表中列出的 Microsoft Windows SDK 文档中介绍了其中所有的 COM 接口的集合。 从应用程序，但作为 WIA 微型驱动程序在同一进程中，在单独的进程中运行 WIA 服务。 应用程序设备将请求定向到 WIA 服务。 WIA 服务然后这些将请求定向到相应的微型驱动程序，通过 WIA 设备驱动程序接口 (WIA DDI)。 下表列出了 WIA 应用程序可以实现的 Api。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA API</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IEnumWIA_DEV_CAPS</strong></p></td>
<td><p>枚举 WIA 硬件设备的功能。 设备功能包括命令和设备支持的事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWIA_DEV_INFO</strong></p></td>
<td><p>枚举 WIA 硬件设备和它们的属性。 设备信息属性描述的安装和配置 WIA 硬件设备。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IEnumWIA_FORMAT_INFO</strong></p></td>
<td><p>枚举设备的格式和媒体类型信息。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWiaItem</strong></p></td>
<td><p>枚举<strong>IWiaItem</strong>树的当前文件夹中的对象。 WIA 运行时系统表示某应用程序作为层次结构树的每个 WIA 硬件设备<strong>IWiaItem</strong>对象。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDataCallback</strong></p></td>
<td><p>提供了在从 WIA 硬件设备到应用程序的数据传输过程中的应用程序回调机制。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaDataTransfer</strong></p></td>
<td><p>支持共享的内存窗口，将数据从设备对象传输到应用程序，并在封送处理期间消除不必要的数据副本。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDevMgr</strong></p></td>
<td><p>应用程序使用它来创建和管理图像获取设备。 他们还使用它来注册以接收设备事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaEventCallback</strong></p></td>
<td><p>由应用程序，用于接收 WIA 硬件设备事件的通知。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaItem</strong></p></td>
<td><p>使应用程序到其功能的查询设备。 <strong>IWiaItem</strong>还提供了对数据传输接口和项属性的访问。 此外，此接口提供了方法，使应用程序来控制设备。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaPropertyStorage</strong></p></td>
<td><p>提供对信息的访问有关<strong>IWiaItem</strong>对象的属性。</p></td>
</tr>
</tbody>
</table>

 

### <a name="wia-driver-services-library"></a>WIA 驱动程序服务库

[WIA 驱动程序服务库](wia-driver-services-library.md)是系统提供的组件，它提供用于 WIA 微型驱动程序的帮助器函数。 微型驱动程序可以调用帮助程序函数来执行任务，如下所示：

-   初始化[WIA 驱动程序项树](wia-driver-item-tree.md)。

-   读取、 写入和验证设备属性。

-   将数据传输。

或者，微型驱动程序可以执行此类任务本身。 使用 helper 函数，可以减少开发时间和 WIA 微型驱动程序的大小，并仍然可以灵活地开发单个解决方案。

### <a name="wia-utility-library"></a>WIA 实用程序库

[WIA 的实用程序库](wia-utility-library.md)包含一系列调试函数 (**wiauDbg * * * Xxx*)，一般实用帮助程序函数和三个类的集合： **CWiauDbgFn**类， **CWiauFormatConverter**类，和**CWiauPropertyList**类。

### <a name="wia-minidrivers"></a>WIA 微型驱动程序

[WIA 微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff545027)供应商提供的是，将 WIA 属性更改和命令指向图像处理设备的用户模式组件。 微型驱动程序实现 WIA DDI WIA 服务调用与微型驱动程序进行通信。

WIA 微型驱动程序提供了为内核模式下仍映像驱动程序，从而推动了图像处理设备的驱动程序，如 USB 驱动程序通过提供特定于设备的用户模式接口。 微型驱动程序与内核模式驱动程序通过调用[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， **ReadFile**， **WriteFile**，和[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) Microsoft Win32 函数 （它们 Microsoft Windows SDK 文档中所述）。

图像处理应用程序不能直接调用 WIA 微型驱动程序。 只有 WIA 服务可以直接调用该驱动程序。

### <a name="kernel-io-drivers"></a>内核 I/O 驱动程序

内核模式下仍映像驱动程序是系统提供的或 IHV 提供包传递到静止图像设备和静止图像设备从传输数据的组件。 内核模式下仍映像驱动程序是特定于总线的。

Microsoft 提供了基于 Microsoft Windows 驱动程序模型 WDM 的内核模式下仍映像驱动程序 USB、 SCSI、 序列和 IEEE 1394 总线。 有关这些驱动程序的详细信息，请参阅[访问内核模式设备驱动程序仍映像](accessing-kernel-mode-drivers-for-still-image-devices.md)。

仅当其成像设备不符合 Microsoft 提供的内核模式 I/O 驱动程序供应商必须提供内核模式下仍映像驱动程序。

**请注意**  上 Windows XP 和更高版本，可以从该驱动程序检索版本信息。 [ **WIA\_DIP\_WIA\_版本**](https://msdn.microsoft.com/library/windows/hardware/ff550296)属性包含 WIA 版本，并且[ **WIA\_DIP\_驱动程序\_版本**](https://msdn.microsoft.com/library/windows/hardware/ff550263)属性包含的驱动程序 DLL 版本。 WIA 服务创建和维护这些属性;则会自动添加 WIA 服务加载驱动程序。 Windows Me 不包括这些属性。

 

 

 




