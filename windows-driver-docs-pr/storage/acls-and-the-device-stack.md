---
title: ACL 和设备堆栈
description: ACL 和设备堆栈
ms.assetid: DAFC851D-E808-4588-86D2-E608584FD05B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd6567b89243c3f685217e250e0a7678c89110cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382750"
---
# <a name="acls-and-the-device-stack"></a>ACL 和设备堆栈


通过设置每个相应的接口的 Acl 控制对该卷和设备的访问权限。 确定设备接口上的 Acl:

-   是否用户会收到请求的访问权限时应用程序请求打开到设备的句柄。

-   哪些命令可以发送到设备。

可移动媒体，如 CD 驱动器的驱动程序堆栈可以具有多个接口：

-   一个与 PDO，由端口驱动程序管理相关联。

-   一个与 FDO，由类驱动程序 (Cdrom.sys) 相关联。

热插拔如 UFD 设备的驱动程序堆栈还为卷管理器提供一个接口。 例如，格式设置实用工具将打开的句柄对卷进行格式化的卷接口。

用于直接访问应用程序可以使用端口驱动程序和类驱动程序接口若要打开的句柄驱动器。 例如，如果应用程序想要通过物理驱动器接口向设备发送的 SCSI 命令，该过程如下所示：

-   应用程序首次打开的句柄驱动器接口，用于读取和写入访问。

-   已成功打开句柄后，可以使用该应用程序[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)函数将 SCSI 请求发送到设备。

当驱动程序堆栈创建的设备接口时，该设备上应用 ACL。 ACL 的访问控制元素 (ACE) 描述的用户组和相关访问权限。 例如，管理员组的 ACE 可能描述了管理员可以为该设备接口的读取和写入访问权限。

当应用程序尝试打开到设备的句柄时，I/O 管理器将使用设备的 ACL 来确定是否允许调用方所请求的访问。 例如，如果调用方请求设备的句柄的读取和写入访问，仅当调用方允许读取和写入通过该接口提供句柄。 如果调用方没有所请求的访问权限，I/O 管理器返回拒绝访问错误，并打开的句柄请求会失败。

这些 Windows 组件创建设备 Acl:I/O 管理器、 即插即用管理器和新的组策略服务为可移动存储设备。

## <a name="span-idiomanagerandremovablemediadeviceaclsspanspan-idiomanagerandremovablemediadeviceaclsspanspan-idiomanagerandremovablemediadeviceaclsspanio-manager-and-removable-media-device-acls"></a><span id="I_O_Manager_and_Removable_Media_Device_ACLs"></span><span id="i_o_manager_and_removable_media_device_acls"></span><span id="I_O_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>I/O 管理器和可移动介质设备 Acl


当驱动程序堆栈创建的设备对象时，I/O 管理器设置默认值取决于设备类型的 ACL。 ACL 授予完全访问权限的默认值为系统和管理员，并且它提供中仅执行对其他人访问。

-   默认情况下，I/O 管理器授予 IU 组完全访问权限，对于设备对象的 CD 驱动器等可移动媒体设备和这些磁盘已定义文件的设备对象\_可移动\_媒体特征。

    **请注意**  在 Windows Vista 之前的条目 IU 未出现在 I/O 管理器已设置的 ACL。 从 Windows Vista 开始，I/O 管理器提供了完整到 IU 组访问权限，以便应用程序可以接收到的卷的直接访问而无需提升权限，如前面所述。 但是，未设置的 UFD 设备**可移动**属性不会得益于这因为 I/O 管理器不会将它们视为可移动。

     

-   磁盘类驱动程序设置的文件\_可移动\_媒体特征 （收到从响应 SCSI 查询命令中的设备） 的标识数据是否有**可移动**属性集。 因为某些 UFD 设备设置此属性，即使它们不是真正可移动介质，I/O 管理器将此类设备视为可移动磁盘，并提供 IU 组读取和写入到卷的访问权限。

-   默认情况下，I/O 管理器仅允许执行访问远程连接的用户的可移动媒体 （CD 设备） 的设备对象和这些磁盘设备对象具有文件\_可移动\_介质特征集。 正因为如此，远程用户不能通过使用 CD 或 DVD 驱动器刻录数据或执行备份到光学介质或格式化可移动磁盘。 管理员可以设置可移动存储访问组策略重写默认行为。 设置此策略，I/O 管理器授予完全访问远程用户对于这些设备，允许读取和写入功能。

## <a name="span-idpnpmanagerandremovablemediadeviceaclsspanspan-idpnpmanagerandremovablemediadeviceaclsspanspan-idpnpmanagerandremovablemediadeviceaclsspanpnp-manager-and-removable-media-device-acls"></a><span id="PnP_Manager_and_Removable_Media_Device_ACLs"></span><span id="pnp_manager_and_removable_media_device_acls"></span><span id="PNP_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>PnP 管理器和可移动介质设备 Acl


当启动设备驱动程序堆栈时，即插即用管理器更改设备上的 ACL 仅当注册表中的设备的项指定该设备的安全描述符。 设备供应商可以通过设置此描述符**SetupDiSetDeviceRegistryProperty**属性设置以下所示。

|          |                                  |
|----------|----------------------------------|
| 属性 | SPDRP\_安全                  |
| 值    | **安全\_描述符**         |
| 大小     | **sizeof**(安全\_描述符) |

 

这些属性还可以将设置通过驱动程序包安装程序，通过在 INF 文件中指定的相关的参数。

## <a name="span-idgrouppolicyserviceforremovablestoragedevicesaclsspanspan-idgrouppolicyserviceforremovablestoragedevicesaclsspanspan-idgrouppolicyserviceforremovablestoragedevicesaclsspangroup-policy-service-for-removable-storage-devices-acls"></a><span id="Group_Policy_Service_for_Removable_Storage_Devices_ACLs"></span><span id="group_policy_service_for_removable_storage_devices_acls"></span><span id="GROUP_POLICY_SERVICE_FOR_REMOVABLE_STORAGE_DEVICES_ACLS"></span>可移动存储设备 Acl 的组策略服务


这是一种 Windows 服务，可让管理员为 CD 或 DVD、 磁带和软盘驱动器和通过组策略框架 WPD 设备磁盘的卷接口和卷接口设置 Acl。 此组策略可以动态更改。 时策略应用到计算机中，服务将更新的设备的 ACL。 此服务采用的 ACL 将覆盖默认值由 I/O 管理器和 PnP 管理器设置的 ACL。

组策略服务上的磁盘的卷接口，但不是在磁盘类驱动程序提供的接口上设置 ACL。 这是因为，当应用程序访问文件和目录的卷上，I/O 管理器使用 ACL 上相应的卷对象来确定调用方是否具有所需的访问权限。 因此，通过在卷设备对象上设置 ACL，组策略服务强制实施管理员为该卷设置的访问权限。

## <a name="span-idsecuritycheckprocessspanspan-idsecuritycheckprocessspanspan-idsecuritycheckprocessspansecurity-check-process"></a><span id="Security_Check_Process"></span><span id="security_check_process"></span><span id="SECURITY_CHECK_PROCESS"></span>安全检查过程


当应用程序尝试打开设备接口的句柄时，I/O 管理器检查用户是否已被授予中请求的访问权限[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)调用。 如果是，打开句柄;否则，调用将失败错误访问\_被拒绝。

打开句柄后，应用程序可以将命令发送到设备，直接通常通过使用 IOCTL。 例如，若要发送 SCSI 传递命令，应用程序将使用**IOCTL\_SCSI\_传递\_THROUGH**或**IOCTL\_SCSI\_传递\_通过\_直接**。

-   **IOCTL\_磁盘\_获取\_分区\_信息**需要只是读取访问权限。

-   **IOCTL\_SCSI\_传递\_THROUGH**并**IOCTL\_SCSI\_传递\_THROUGH\_直接**要求对调用方已为读取和写入访问权限打开的句柄 （这由存储设备驱动程序） 的接口。

SCSI 传递请求中提供了命令描述符块 (CDB) 中的操作码不检查以确定是否需要读取、 写入、，或读取和写入访问。 这是 Windows 始终需要设备要打开以进行读取和写入，传递请求的句柄，即使应用程序仅执行读取、 写入或无数据传输根本原因。

**IOCTL\_磁盘\_验证**可以不考虑中请求了的访问权限的情况下发送[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)调用。 当 I/O 管理器收到 IOCTL 时，它会检查该 IOCTL 所需的访问权限，并将其与在调用方授予访问权限进行比较**CreateFile**调用。 如果没有匹配项，IOCTL 发送到目标设备;否则，IOCTL 调用失败，错误访问\_被拒绝。

例如，如果调用方已打开的句柄的只读访问权限，如下所示。

-   **IOCTL\_SCSI\_传递\_THROUGH**失败，出现错误访问\_拒绝，因为它需要读取和写入访问。

-   **IOCTL\_磁盘\_获取\_分区\_信息**发送到驱动程序堆栈，因为它需要只读访问权限。

 

 




