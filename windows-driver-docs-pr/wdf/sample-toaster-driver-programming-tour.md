---
title: 示例 Toaster 驱动程序编程指南
description: 本主题提供了 Toaster 示例的代码演练，其中包含为学习目的而设计的内核模式驱动程序框架（KMDF）和用户模式驱动程序框架（UMDF）驱动程序。
ms.assetid: 5977AC09-AB53-4CA4-A35A-0E5A1FEE936F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a248f805a01d025eed0262160b68c5151f3c7ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842197"
---
# <a name="sample-toaster-driver-programming-tour"></a>示例 Toaster 驱动程序编程指南


本主题提供了[Toaster](https://go.microsoft.com/fwlink/p/?LinkId=618939)示例的代码演练，其中包含为学习目的而设计的内核模式驱动程序框架（KMDF）和用户模式驱动程序框架（UMDF）驱动程序。

## <a name="class-installer-and-coinstaller"></a>类安装程序和 Coinstaller


Tostrcls 项目演示如何编写类安装程序 DLL。 此 DLL 为 Toaster 类提供了一个自定义图标，**设备管理器**中的自定义属性表可更改设备的友好名称。 此 DLL 在 toaster 的 INF 文件中引用。

Tostrco1 项目演示如何编写 coinstaller DLL。 此 DLL 显示了如何基于设备的实例编号创建友好名称，以及如何分析 INF 文件中的自定义部分。 此 DLL 在 toaster 的 INF 文件中引用。

## <a name="applications"></a>应用程序


该示例包括与 toaster 总线驱动程序和函数驱动程序交互的应用程序。 这些应用程序适用于 KMDF 和 UMDF toaster 版本。

-   Enum 是一个简单的控制台应用程序的用户模式枚举器。 由于 toaster 总线不是物理总线，因此你可以使用此应用程序来使总线驱动程序插入、拔出和弹出系统中的设备。 键入 Enum 作为使用提示。
-   Toast：这是用于控制 toaster 的用户模式控制台应用程序。 此应用程序枚举 toaster 设备，打开上一个枚举设备，并向其发送读取请求。
-   Notepad.exe：此 GUI 应用程序结合了 Enum 和 appcmd.exe 的功能，并演示了如何在用户模式下处理 PnP 通知。 例如，使用 toastco 安装 toaster 的 coinstaller，并使用此应用来查看 PnP 通知。 你还可以使用 Notify 来指定不同的硬件 ID （默认 toaster 设备 ID 除外），以使其他驱动程序作为函数驱动程序加载。

## <a name="kmdf-bus-driver"></a>KMDF 总线驱动程序


KMDF 总线驱动程序为 toaster 总线控制器服务，枚举接通电源的设备，并执行总线级别电源管理。 总线驱动程序支持 D0 和 D3 电源状态。 它还具有 WMI 接口。 此目录包含两个显示 Toaster 总线驱动程序的两种不同实现的子目录。

- **静止**

  总线驱动程序的静态版本演示了如何使用静态子列表（每个设备提供一个）枚举子设备，该列表由框架提供。

  利用*静态枚举*，驱动程序可以在初始化期间检测和报告设备是否存在，并具有对系统配置的后续更改的有限能力。

  如果设备或功能子单元连接的数量和类型是预先确定的并且是永久性的，并且不依赖于运行驱动程序的系统的配置，则总线驱动程序可以使用静态枚举。

  例如，声卡的驱动程序可以充当总线驱动程序，并为每个卡的功能创建单独的物理设备对象（PDOs），如 MIDI、音频和游戏杆。

  若要枚举子总线驱动程序，请执行以下操作：

  1.  调用[**WdfPdoInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)以获取[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构。

  2.  初始化[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构。

  3.  调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建表示 PDO 的框架设备对象。

  调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之后，驱动程序将调用[**WdfFdoAddStaticChild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoaddstaticchild) ，将子设备添加到子列表中。

  由于驱动程序只应为预先确定和永久的设备配置使用静态子列表，因此，驱动程序通常不会在创建后修改静态子列表。 如果驱动程序确定子设备不可访问，则驱动程序可以调用[**WdfPdoMarkMissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdomarkmissing)。 （如果子设备可以访问但没有响应，则驱动程序应将[**WDF\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)结构的**失败**成员设置为**WdfTrue** ，然后调用[**WdfDeviceSetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)。）

  若要在每次总线驱动程序启动时静态枚举子设备，可在 Toaster Bus 驱动程序的设备参数密钥中设置注册表值。

  **HKEY\_本地\_计算机\\系统\\CurrentControlSet\\枚举\\根\\SYSTEM\\&lt;InstanceNumber&gt;\\设备参数**

  **NumberOfToasters： REG\_DWORD：2**

  使用此注册表设置可以枚举的子设备的最大数目为10。 还可以通过 Toaster Bus Inf 文件配置此值。

- **动态**

  总线驱动程序的动态版本演示了如何使用子列表对象枚举子设备。

  使用*动态枚举*，驱动程序可以检测和报告在系统运行时连接到系统的设备的数量和类型的更改。

  如果连接到父设备的设备数取决于系统的配置，则总线驱动程序必须使用动态枚举。 其中一些设备可能始终连接到系统，某些设备可能会在系统运行时插入并拔下。

  例如，插入到系统 PCI 总线中的设备的数量和类型与系统相关，但它们是永久性的，除非用户关闭电源、打开机箱，并使用螺丝刀添加或删除设备。 另一方面，在系统运行时，用户可以通过插入或拔出电缆来添加或删除 USB 设备。

  每次总线驱动程序标识子设备时，它必须将子设备的说明添加到子列表中。 驱动程序可以通过调用[**WdfFdoGetDefaultChildList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdogetdefaultchildlist)来使用框架提供的设备的默认子列表，也可以通过调用[**WdfChildListCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistcreate)创建其他子列表来分组子列表。 此示例使用默认的子列表。 *子说明*由所需的*标识说明*和可选*地址说明*组成。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">术语</th>
  <th align="left">描述</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="" id="---------------------identification-description"></a>标识描述</p></td>
  <td align="left"><p>标识说明是一个结构，其中包含用于唯一标识驱动程序所枚举的每个设备的信息。 驱动程序定义此结构，但其第一个成员必须是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header)"><strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong></a>结构。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="" id="---------------------address-description"></a>地址说明</p></td>
  <td align="left"><p>地址说明是一个结构，其中包含驱动程序所需的信息，以便在设备接通电源的情况下可以在设备总线上访问设备。 驱动程序定义此结构，但其第一个成员必须是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header)"><strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong></a>结构。 地址说明是可选的。 此示例不使用地址说明。</p></td>
  </tr>
  </tbody>
  </table>




若要向子列表添加子级，驱动程序将为它找到的每个子设备调用[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) 。 此调用通知框架驱动程序已发现连接到父设备的子设备。 当你的驱动程序调用**WdfChildListAddOrUpdateChildDescriptionAsPresent**时，它将提供标识说明并根据需要提供地址说明。

驱动程序调用[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)来报告新设备后，框架会通知 PnP 管理器新设备已存在。 然后，PnP 管理器将为新设备生成设备堆栈和驱动程序堆栈。 作为此过程的一部分，框架将调用总线驱动程序的[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数。 此回调函数必须调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)来创建新设备的 PDO。

若要报告缺少的子设备，此驱动程序将调用 WdfChildListUpdateChildDescriptionAsMissing。 有关动态枚举的更多详细信息，请参阅框架文档。


## <a name="kmdf-function-driver"></a>KMDF 函数驱动程序


函数驱动程序有两个不同的版本： wdfsimple 和 wdffeatured。 函数驱动程序的两个版本在*共享*目录中共享一个公共标头文件。

-   **WdfSimple**

    在此版本中，驱动程序不会处理任何 PnP 和电源事件，而是依赖于框架的对这些事件的默认支持。 应用程序（如 notepad.exe）可以使用此驱动程序打开驱动程序注册的设备接口，并发送读取、写入或 IOCTL 请求。

-   **WdfFeatured**

    此版本演示如何注册 PNP 和电源事件，处理创建和关闭文件请求，处理 WMI 集和查询事件，并触发 WMI 通知事件。 作为电源策略所有者，它还会注册空闲通知，以便在没有 i/o 活动时将设备置于低功耗状态。

## <a name="kmdf-filter-driver"></a>KMDF 筛选器驱动程序


此目录包含两个筛选器驱动程序的源代码。 一般示例是一个简单的 passthru 筛选器驱动程序。 SideBand 演示如何使用控制设备对象向应用程序提供 SideBand ioctl 接口。 此专用接口使应用程序能够直接与筛选器驱动程序通信;绕过筛选器附加到的功能设备堆栈。 SideBand 示例还演示了当驱动程序将处理多个设备的请求时，如何实现设备对象的集合。 可以通过使用 toaster 在现有的设备上安装这些筛选器。

## <a name="kmdf-toastmon"></a>KMDF Toastmon


此示例演示如何使用远程 i/o 目标接口打开设备并在内核模式下执行 i/o。 此示例通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)为 toaster 接口类注册 PnP 通知回调例程。 当 toaster 设备接通电源时，PnP 管理器将调用该回调。 在回调中，此示例创建一个远程目标，并使用回调数据中提供的符号链接打开该设备。

此外，此示例还使用被动计时器演示对目标设备的异步读取和写入。 它还演示了如何通过在 i/o 目标对象上注册[*EvtIoTargetQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)/[*EvtIoTargetRemoveCanceled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)/[*EvtIoTargetRemoveComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)来响应设备更改通知。 如果驱动程序与驱动程序未控制的另一台设备通信，则可以使用此方法。 使用 Wdftoastmon 将此驱动程序安装为根枚举设备。 使用与 toaster 总线驱动程序相同的安装步骤。

## <a name="umdf-function-driver"></a>UMDF 函数驱动程序


WUDFToaster 驱动程序使用户应用程序（toast/notify）能够打开驱动程序注册的设备接口，并发送读取、写入或 IOCTL 请求。 此驱动程序示例还演示了如何注册 PnP 和电源事件、设置电源策略所有权并处理 i/o 请求。 这是不应在生产环境中使用的最小驱动程序示例。

可以将 WUDF Toaster 与 KMDF Toastmon 示例结合使用，以演示内核模式客户端使用远程 i/o 目标访问用户模式驱动程序的权限。

为此，请将以下行添加到。此 UMDF 驱动程序 INF 的 WDF 部分： **UmdfKernelModeClientPolicy = AllowKernelModeClients**

### <a name="testing-umdf-toaster"></a>测试 UMDF Toaster

1.  使用 cscript.exe、Notify .exe 或 Enum 应用程序。
2.  安装 KMDF Toastmon 驱动程序。 如前文所述，允许内核模式客户端到用户模式驱动程序。 安装 WUDFToaster。 使用 Traceview 查看从 Toastmon 发送到 UMDF Toaster 的请求。

### <a href="" id="umdf-toastmon"></a>UMDF Toastmon 概述

此示例是 KMDF ToastMon 示例的 UMDF 版本。

UMDF Toastmon 演示了如何使用 UMDF 通过用户模式驱动程序框架编写最小的驱动程序，并演示最佳做法。 驱动程序将在设备（根枚举或真实硬件设备）上成功加载，但具有最低 PnP 功能，并且不支持接收任何 i/o 操作。

Toastmon 旨在用作一种学习工具，供你编写的其他 UMDF 驱动程序使用。









