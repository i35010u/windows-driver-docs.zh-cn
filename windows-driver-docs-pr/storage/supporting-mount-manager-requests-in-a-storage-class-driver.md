---
title: 支持存储类驱动程序中的装入管理器请求
description: 支持存储类驱动程序中的装入管理器请求
ms.assetid: fb37f862-70d6-4514-b481-16f664346422
keywords:
- 存储类驱动程序 WDK，计数管理器
- 类驱动程序 WDK 存储计数管理器
- 计数管理器 WDK 存储
- MM WDK 存储
- 卷名称 WDK 存储
- 名称 WDK 存储
- 唯一的卷名称 WDK 存储
- 永久名称数据库 WDK 存储
- MountedDevices
- 死信装入的设备 WDK 存储
- 符号链接名称 WDK 存储
- 非持久性名称 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a05bb94b0be40e790074ee82ddcef48fb6d52160
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342194"
---
# <a name="supporting-mount-manager-requests-in-a-storage-class-driver"></a>支持存储类驱动程序中的装入管理器请求


## <span id="ddk_supporting_mount_manager_requests_in_a_storage_class_driver_kg"></span><span id="DDK_SUPPORTING_MOUNT_MANAGER_REQUESTS_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


装入管理器 （毫米） 是负责管理卷名称。 对于每个卷，它将存储都是唯一且永久标识与该卷，即使从系统中删除该卷的名称。 它还管理不太永久名称，如在重新启动后，保留的但添加到或从系统中删除卷时，可以更改其分配的驱动器号。

计数管理器创建卷的设备对象的符号链接，系统中提供的每个卷的唯一接口。 由于符号链接本身和它们针对的对象不会保留在系统重新启动时的设备，则计数管理器保留*名称*符号链接中的*永久名称数据库*中在注册表中。

此符号链接名称被称为*唯一卷名称*。 像是传统的卷标签，它仍然存在时系统重新启动，但如驱动器号，并且与不同的卷标，它是唯一的。 唯一卷名称的格式为：

"**\\??\\卷 {**<em>GUID</em>**}\\**

其中*GUID*是确定的卷的全局唯一标识符。

装入管理器的永久名称数据库位于**MountedDevices**注册表项的系统配置单元 (**HKLM/SYSTEM/MountedDevices**) 的注册表。 除了唯一卷名称，则计数管理器还存储*装入点*其永久名称数据库中的名称。 装入点名称可以进一步细分为两个类别：用作已装载的卷的文件系统的根目录和驱动器号的 Win32 样式路径名。

在数据库中每个持久性的符号链接名称显示为下的注册表值的名称**MountedDevices**密钥伴随*唯一 ID*。 唯一 ID 是卷的另一个唯一标识符 （唯一的卷名称不同）。 它可帮助识别哪些潜在大量永久符号链接名称引用同一个卷。

例如，单个卷使用的唯一卷名称<strong>"\\\\？\\卷 {</strong>7603f260-142a-11d4-ac67-806d6172696f **}\\"** 可能随附的驱动器号"\\DosDevices\\d:"和两个装入点"\\DosDevices\\c:\\mymount"和"\\DosDevices\\e:\\FilesysD\\mnt"。 这将产生装入管理器的持久性的符号链接名称数据库中的四个条目： 一个用于唯一卷名称，一个驱动器号，两个的两个装入点的名称。 所有四个条目将共享相同的唯一 id。因此有人查看**MountedDevices**注册表项将能够检测到所有四个持久名称是否指向同一个卷。

下面的屏幕截图演示了如何永久名称出现在**MountedDevices**注册表项。

![演示如何持久名称显示在 mounteddevices 注册表项的屏幕截图](images/mntmgr.png)

计数管理器依赖于插设备接口通知机制来提醒的卷到达和删除它。 因此每个客户端 （即，每个卷驱动程序，通常类驱动程序） 必须创建接口 MOUNTDEV\_已装载\_设备\_GUID 接口类通过调用[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)以通知它所管理的卷的系统中到达的装入管理器。 MOUNTDEV\_已装载\_设备\_GUID 接口类中定义 GUID *mountmgr.h*。

收到的卷接口到达插通知时，装入管理器发送客户端三个设备控制 Irp:

* [**IOCTL\_MOUNTDEV\_查询\_设备\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff560437)
* [**IOCTL\_MOUNTDEV\_查询\_UNIQUE\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff560441)
* [**IOCTL\_MOUNTDEV\_查询\_建议\_链接\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff560440)

在以下三个 Ioctl 响应客户端应该返回卷的非持久性设备对象名称 （或目标名称） 位于中**设备**系统对象树的目录 (例如："\\设备\\HarddiskVolume1")，唯一的卷 ID，并建议持久的符号链接名称对于卷，分别。 尽管客户端可能会选择将忽略[ **IOCTL\_MOUNTDEV\_查询\_建议\_链接\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff560440)，会要求他们提供唯一的卷 ID 时接收[ **IOCTL\_MOUNTDEV\_查询\_设备\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff560437)或 IOCTL\_MOUNTDEV\_查询\_UNIQUE\_id。 计数管理器完全依赖于客户端提供唯一的卷 ID，并且如果客户端未提供它，然后装入管理器不能分配给卷的装入点，例如驱动器号。

有关这些 Ioctl 的详细信息，请参阅[I/O 控制代码发送由计数管理器](https://msdn.microsoft.com/library/windows/hardware/ff561594)。

如果客户端警报到达其卷的装入管理器，但无法提供的唯一 ID 的查询时的卷，卷上放置*死信装入的设备*列表。 在这种情况，客户端可以发送[ **IOCTL\_MOUNTMGR\_检查\_UNPROCESSED\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff560454) IOCTL 到装入管理器的请求装入管理器重新扫描其死信已装载的设备列表，并再次尝试查询列表上的客户端用于其各自卷的唯一 Id。 详细了解 IOCTL\_MOUNTMGR\_xxx Ioctl，请参阅[I/O 控制代码发送装载 Manager 客户端](https://msdn.microsoft.com/library/windows/hardware/ff561593)

装载后管理器收到唯一卷 ID 对于新引入的卷，然后搜索其数据库进行所有永久分配给该唯一 ID 的名称，并创建符号链接到每个持久性的符号链接名称的卷。

当计数管理器检测到，卷已脱机然后删除符号链接指向的设备对象而不会删除计数管理器的数据库中相应的符号链接名称。

有关如何装入管理器客户端创建持久的符号名称的信息，请参阅[ **IOCTL\_MOUNTMGR\_创建\_点**](https://msdn.microsoft.com/library/windows/hardware/ff560457)。

 

 




