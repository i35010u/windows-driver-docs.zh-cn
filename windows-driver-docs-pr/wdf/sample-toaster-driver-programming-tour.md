---
title: 示例 Toaster 驱动程序编程简介
description: 本主题提供 Toaster 示例，其中包含出于学习目的而设计的内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序代码的演练。
ms.assetid: 5977AC09-AB53-4CA4-A35A-0E5A1FEE936F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23706c4a4736d6911f3369ba062cbb1ceae8fe92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544211"
---
# <a name="sample-toaster-driver-programming-tour"></a>示例 Toaster 驱动程序编程简介


本主题提供的代码演练[Toaster](https://go.microsoft.com/fwlink/p/?LinkId=618939)示例，其中包含出于学习目的而设计的内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序。

## <a name="class-installer-and-coinstaller"></a>安装程序类和共同安装程序


Tostrcls 项目演示如何编写类安装程序 DLL。 此 DLL 为 Toaster 类和自定义属性表中的提供了一个自定义图标**设备管理器**若要更改设备的友好名称。 为 toaster INF 文件中引用此 DLL。

Tostrco1 项目演示如何编写共同安装程序 DLL。 如何创建基于设备的实例数目的友好名称以及如何分析 INF 文件中的自定义部分显示了此 DLL。 为 toaster INF 文件中引用此 DLL。

## <a name="applications"></a>应用程序


该示例包括与 toaster 总线驱动程序和功能驱动程序进行交互的应用程序。 这些应用程序适用于 KMDF 和 UMDF toaster 版本。

-   Enum.exe 是用户模式枚举器的简单控制台应用程序。 因为 toaster 总线不是物理总线，你可以使用此应用程序导致总线驱动程序插入、 拔出，并弹出从系统的设备。 有关使用情况的提示键入 Enum.exe。
-   Toast.exe:这是用户模式下的控制台应用程序来控制 toaster。 此应用程序枚举 toaster 设备，打开最后一个枚举的设备，并将读取的请求发送到它。
-   Notify.exe:此 GUI 应用程序组合 Enum.exe 和 toast.exe 的功能，并还演示了如何处理在用户模式下的即插即用通知。 例如，安装 toaster 的共同安装程序使用 toastco.inf，并使用此应用查看即插即用通知。 Notify.exe 还可用于指定不同的硬件 ID （而不是默认 toaster 设备 ID) 会导致不同的驱动程序加载为功能驱动程序。

## <a name="kmdf-bus-driver"></a>KMDF 总线驱动程序


KMDF 总线驱动程序服务 toaster 总线控制器、 枚举已接通的设备并执行 bus 级别电源管理。 总线驱动程序支持 D0 和 D3 电源状态。 它还具有一个 WMI 接口。 此目录包含显示 Toaster 总线驱动程序的两个不同的实现的两个子目录。

- **Static**

  总线驱动程序的静态版本演示如何枚举子设备使用静态子列表中，每个设备，框架提供的一个。

  *静态枚举*启用驱动程序以检测和报告的设备是否存在初始化过程中，具有有限能力报告对系统的配置的后续更改。

  如果的数量和类型的设备或功能的子单元连接的预设的且永久性的并且不依赖于系统驱动程序正在其运行的配置，总线驱动程序可以使用静态的枚举。

  例如，声卡的驱动程序可能会充当总线驱动程序，并为每个卡的功能，例如 MIDI，音频和游戏杆创建单独的物理设备对象 (PDOs)。

  若要枚举子，总线驱动程序：

  1.  调用[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)若要获取[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。

  2.  初始化[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。

  3.  调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)创建一个表示 PDO framework 设备对象。

  在调用[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)，驱动程序调用[ **WdfFdoAddStaticChild** ](https://msdn.microsoft.com/library/windows/hardware/ff547225)将子设备添加到子列表。

  因为驱动程序应仅使用静态子列出的预先确定的设备配置并永久性的驱动程序不会通常修改静态子列表创建它后。 如果该驱动程序确定子设备变得不可访问，该驱动程序可以调用[ **WdfPdoMarkMissing**](https://msdn.microsoft.com/library/windows/hardware/ff548809)。 (如果子设备可访问，但无响应，该驱动程序应设置**失败**的成员[ **WDF\_设备\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff551284)结构向**WdfTrue** ，然后调用[ **WdfDeviceSetDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff546884)。)

  若要以静态方式枚举子设备每次总线驱动程序启动时，可以设置注册表值，Toaster 总线驱动程序的设备参数项中。

  **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\Root\\SYSTEM\\&lt;InstanceNumber&gt;\\Device Parameters**

  **NumberOfToasters:REG\_DWORD:2**

  可以使用此注册表设置枚举子设备的最大数目为 10。 此外可以通过 Toaster 总线 Inf 文件中配置此值。

- **Dynamic**

  总线驱动程序的动态版本演示如何枚举子设备使用子列表对象。

  *动态枚举*启用驱动程序以检测和报告到的数量和类型的系统运行时连接到系统的设备的更改。

  如果的数量或连接到父设备的设备的类型取决于系统的配置，总线驱动程序必须使用动态枚举。 这些设备的一些可能始终连接到系统，以及一些可能已插入和拔出系统运行时。

  例如的数量和类型的插入到系统的 PCI 总线的设备是依赖于系统的但它们是永久的除非用户关闭电源、 打开这种情况，并添加或删除设备时使用螺丝刀。 但是，用户可以添加或删除 USB 设备插入或拔出电缆系统运行时。

  每次总线驱动程序标识子设备，它必须将子设备的说明添加到子列表。 驱动程序可以通过调用使用框架提供设备的默认子列表[ **WdfFdoGetDefaultChildList**](https://msdn.microsoft.com/library/windows/hardware/ff547235)，或者可以创建其他子列表中，分组子对象，通过调用[**WdfChildListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545615)。 此示例使用默认子列表。 一个*子描述*由必需*标识说明*和可选*解决说明*。

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
  <td align="left"><p><a href="" id="---------------------identification-description"></a> 标识说明</p></td>
  <td align="left"><p>标识描述是一种结构，其中包含唯一标识该驱动程序枚举每个设备的信息。 该驱动程序定义了此结构，但其第一个成员必须是<a href="https://msdn.microsoft.com/library/windows/hardware/ff551223" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551223)"> <strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong> </a>结构。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="" id="---------------------address-description"></a> 地址说明</p></td>
  <td align="left"><p>地址描述是一种结构，其中包含驱动程序要求，以便它可以访问其总线上的设备，如果在插入设备时，可以更改信息的信息。 该驱动程序定义了此结构，但其第一个成员必须是<a href="https://msdn.microsoft.com/library/windows/hardware/ff551223" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551223)"> <strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong> </a>结构。 地址说明是可选的。 此示例不使用地址说明。</p></td>
  </tr>
  </tbody>
  </table>




若要添加到子列表时，驱动程序调用的子[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)为每个找到的子设备。 此调用会通知框架驱动程序已发现的子设备连接到父设备。 当您的驱动程序调用**WdfChildListAddOrUpdateChildDescriptionAsPresent**，它会提供一个标识说明和地址描述 （可选）。

驱动程序调用后[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)若要报告的新设备，该框架将告知存在新的设备的即插即用管理器。 PnP 管理器然后构建设备堆栈和新设备的驱动程序堆栈。 作为此过程的一部分，框架将调用总线驱动程序[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)回调函数。 必须调用此回调函数[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)若要创建的新设备 PDO。

若要报告子设备丢失，此驱动程序调用 WdfChildListUpdateChildDescriptionAsMissing。 动态枚举的更多详细信息，请参阅框架文档。


## <a name="kmdf-function-driver"></a>KMDF 功能驱动程序


功能驱动程序有两个不同版本： wdfsimple 和 wdffeatured。 功能驱动程序的两个版本共享公共头文件中的*共享*目录。

-   **WdfSimple**

    在此版本中，该驱动程序不会处理任何 PnP 和电源事件，并改为依赖框架的默认支持这些事件。 应用程序，例如 notify.exe，可以使用此驱动程序打开驱动程序已注册的设备接口并发送读取、 写入或 IOCTL 请求。

-   **WdfFeatured**

    此版本演示如何注册 PNP 和电源事件，处理创建和关闭文件请求、 处理 WMI 集和查询事件，并触发 WMI 通知事件。 通过电源策略所有者，它还会注册空闲通知以便它可以将设备到低功耗状态时没有任何 I/O 活动。

## <a name="kmdf-filter-driver"></a>KMDF 筛选器驱动程序


此目录包含两个筛选器驱动程序的源代码。 泛型示例是一个简单的 passthru 筛选器驱动程序。 旁带演示如何通过使用控制设备对象提供对应用程序旁带 ioctl 接口。 此专用接口使应用程序直接调用与筛选器驱动程序绕过功能设备堆栈，该筛选器附加到。 旁带示例还演示如何实现的设备对象的集合，如果该驱动程序将处理多个设备的请求。 通过使用 filter.inf，可以在现有的 toaster 设备上安装这些筛选器。

## <a name="kmdf-toastmon"></a>KMDF Toastmon


此示例演示如何打开设备并在内核模式下使用远程 I/O 目标接口执行 I/O。 此示例将通过调用注册 toaster 接口类的即插即用通知回调例程[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)。 当在插入 toaster 设备时，即插即用管理器调用的回调。 在回调中，此示例创建一个远程目标，并通过使用提供的回调数据中的符号链接打开设备。

此外，此示例使用被动计时器演示异步读取和写入到目标设备。 它还演示如何通过注册来响应设备更改通知[ *EvtIoTargetQueryRemove*](https://msdn.microsoft.com/library/windows/hardware/ff541793)/[*EvtIoTargetRemoveCanceled* ](https://msdn.microsoft.com/library/windows/hardware/ff541800) / [ *EvtIoTargetRemoveComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff541806) I/O 的目标对象。 如果您的驱动程序与您的驱动程序不能控制的另一台设备，可以使用此技术。 为使用 Wdftoastmon.inf 根枚举设备安装此驱动程序。 用于作为 toaster 总线驱动程序安装使用相同的步骤。

## <a name="umdf-function-driver"></a>UMDF 功能驱动程序


WUDFToaster 驱动程序，以打开驱动程序已注册的设备接口并发送读取、 写入或 IOCTL 请求的用户应用程序 (toast/notify.exe)。 此驱动程序示例还演示如何注册 PnP 和电源事件，设置电源策略所有权，并处理 I/O 请求。 这是不适合在生产环境中使用的最小的驱动程序示例。

可以使用 WUDF Toaster 与 KMDF Toastmon 示例结合使用，以演示如何对使用远程 I/O 目标的用户模式驱动程序的内核模式下客户端访问。

若要执行此操作，添加下面的代码行。WDF 部分中的此 UMDF 驱动程序的 INF:**UmdfKernelModeClientPolicy = AllowKernelModeClients**

### <a name="testing-umdf-toaster"></a>测试 UMDF Toaster

1.  使用 Toast.exe、 Notify.exe 或 Enum.exe 应用程序。
2.  安装 KMDF Toastmon 驱动程序。 允许用户模式驱动程序如前面所述的内核模式下客户端。 安装 WUDFToaster.dll。 使用 Traceview.exe 查看从 Toastmon 发送到 UMDF Toaster 的请求。

### <a href="" id="umdf-toastmon"></a>UMDF Toastmon 概述

此示例是 KMDF ToastMon 示例的 UMDF 版本。

UMDF Toastmon 演示如何使用 UMDF 编写最少驱动程序使用用户模式驱动程序框架，并演示最佳实践。 驱动程序已成功将设备 （枚举的根或实际硬件设备） 上加载但已最小的即插即用功能并不支持接收任何 I/O 操作。

Toastmon 旨在作为学习工具，可以编写其他 UMDF 驱动程序。









