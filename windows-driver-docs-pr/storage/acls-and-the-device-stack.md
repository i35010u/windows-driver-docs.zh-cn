---
title: ACL 和设备堆栈
description: ACL 和设备堆栈
ms.assetid: DAFC851D-E808-4588-86D2-E608584FD05B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c20f527b205391ffdb0878558c82681b911f4858
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968428"
---
# <a name="acls-and-the-device-stack"></a>ACL 和设备堆栈


卷和设备的访问权限由在各自每个接口上设置的 Acl 控制。 设备接口上的 Acl 确定：

-   当应用程序请求打开设备的句柄时，用户是否收到请求的访问权限。

-   可以向设备发送哪些命令。

可移动媒体（如 CD 驱动器）的驱动程序堆栈可以有多个接口：

-   一个与 PDO 关联的，由端口驱动程序管理。

-   与 FDO 关联的一个，它由类驱动程序（Cdrom.sys）进行管理。

适用于热插拔设备的驱动程序堆栈（如 UFD）还提供了一个到卷管理器的接口。 例如，格式化实用工具将为卷接口打开一个句柄，以对卷进行格式化。

对于直接访问，应用程序可以使用端口驱动程序和类驱动程序接口打开驱动器的句柄。 例如，如果应用程序想要通过物理驱动器接口将 SCSI 命令发送到设备，则该过程如下所示：

-   应用程序首先打开驱动器接口的句柄，以便进行读写访问。

-   成功打开句柄后，应用程序可以使用[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数将 SCSI 请求发送到设备。

当驱动程序堆栈创建设备接口时，将在该设备上应用 ACL。 ACL 的访问控制元素（ACE）描述了用户组和相关的访问权限。 例如，Administrators 组的 ACE 可能描述管理员对该设备接口具有的读取和写入访问权限。

当应用程序尝试打开设备的句柄时，i/o 管理器使用设备的 ACL 来确定是否允许调用方访问请求的访问权限。 例如，如果调用方请求设备的句柄进行读写访问，则仅当调用方可以通过该接口进行读取和写入时，才提供句柄。 如果调用方没有请求的访问权限，则 i/o 管理器会返回拒绝访问错误，打开句柄请求会失败。

设备 Acl 由以下 Windows 组件创建： i/o 管理器、PnP 管理器和适用于可移动存储设备的新组策略服务。

## <a name="span-idi_o_manager_and_removable_media_device_aclsspanspan-idi_o_manager_and_removable_media_device_aclsspanspan-idi_o_manager_and_removable_media_device_aclsspanio-manager-and-removable-media-device-acls"></a><span id="I_O_Manager_and_Removable_Media_Device_ACLs"></span><span id="i_o_manager_and_removable_media_device_acls"></span><span id="I_O_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>I/o 管理器和可移动媒体设备 Acl


当驱动程序堆栈创建设备对象时，i/o 管理器会根据设备类型设置默认 ACL。 默认 ACL 提供对系统和管理员的完全访问权限，并且仅授予对其他人的执行访问权限。

-   默认情况下，i/o 管理器授予对可移动媒体设备（如 CD 驱动器）的设备对象的完全访问权限，并为那些已定义文件 \_ 可移动媒体特征的磁盘设备对象授予完全访问权限 \_ 。

    **注意**   在 Windows Vista 之前，已由 i/o 管理器设置的 ACL 中不存在 IU 的条目。 从 Windows Vista 开始，i/o 管理器提供对 IU 组的完全访问权限，以便应用程序无需提升权限即可直接访问卷，如前文所述。 但是，没有设置**可移动**属性的 UFD 设备不会从这种情况中受益，因为 i/o 管理器不会将它们视为可移动。

     

-   \_ \_ 如果标识数据（从设备收到的响应 SCSI 查询命令）具有**可移动**属性集，则磁盘类驱动程序将设置文件可移动介质特性。 由于某些 UFD 设备即使不是真正的可移动媒体，也设置此属性，因此，i/o 管理器会将此类设备视为可移动磁盘，并为 IU 组提供对卷的读写访问权限。

-   默认情况下，i/o 管理器仅向远程连接的用户提供可移动媒体设备对象（CD 设备）的执行访问权限，并为那些具有文件 \_ 可移动 \_ 媒体特征集的磁盘设备对象提供执行访问权限。 因此，远程用户无法通过使用 CD 或 DVD 驱动器刻录数据或执行到光学媒体的备份或格式化可移动磁盘。 管理员可以设置可移动存储访问组策略来覆盖默认行为。 设置此策略后，i/o 管理器将为这些设备授予远程用户完全访问权限，允许读取和写入功能。

## <a name="span-idpnp_manager_and_removable_media_device_aclsspanspan-idpnp_manager_and_removable_media_device_aclsspanspan-idpnp_manager_and_removable_media_device_aclsspanpnp-manager-and-removable-media-device-acls"></a><span id="PnP_Manager_and_Removable_Media_Device_ACLs"></span><span id="pnp_manager_and_removable_media_device_acls"></span><span id="PNP_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>PnP 管理器和可移动媒体设备 Acl


当设备驱动程序堆栈启动时，只有当设备在注册表中的密钥为该设备指定了安全描述符时，PnP 管理器才会更改设备上的 ACL。 设备供应商可以使用**SetupDiSetDeviceRegistryProperty**设置此描述符，并将属性设置为，如下所示。

**属性**： SPDRP \_ 安全性

**值**：**安全 \_ 描述符**

**Size**： **sizeof**（安全 \_ 描述符）


 

这些属性还可以通过驱动程序包安装程序进行设置，方法是在 INF 文件中指定相关参数。

## <a name="span-idgroup_policy_service_for_removable_storage_devices_aclsspanspan-idgroup_policy_service_for_removable_storage_devices_aclsspanspan-idgroup_policy_service_for_removable_storage_devices_aclsspangroup-policy-service-for-removable-storage-devices-acls"></a><span id="Group_Policy_Service_for_Removable_Storage_Devices_ACLs"></span><span id="group_policy_service_for_removable_storage_devices_acls"></span><span id="GROUP_POLICY_SERVICE_FOR_REMOVABLE_STORAGE_DEVICES_ACLS"></span>适用于可移动存储设备的组策略服务 Acl


这是一种 Windows 服务，它允许管理员通过组策略框架为磁盘和 CD 或 DVD、磁带和软盘驱动器以及 WPD 设备的卷接口设置 Acl。 可以动态更改此组策略。 将策略应用到计算机后，服务会更新设备的 ACL。 此服务应用的 ACL 将覆盖由 i/o 管理器和 PnP 管理器设置的默认 ACL。

组策略服务在卷接口上为磁盘设置 ACL，而不是在提供磁盘类驱动程序的接口上设置。 这是因为，当应用程序访问卷上的文件和目录时，i/o 管理器将在相应的卷对象上使用 ACL 来确定调用方是否具有所需的访问权限。 因此，通过在卷设备对象上设置 ACL，组策略服务将强制管理员为该卷设置的访问权限。

## <a name="span-idsecurity_check_processspanspan-idsecurity_check_processspanspan-idsecurity_check_processspansecurity-check-process"></a><span id="Security_Check_Process"></span><span id="security_check_process"></span><span id="SECURITY_CHECK_PROCESS"></span>安全检查过程


当应用程序尝试打开设备接口的句柄时，i/o 管理器会检查是否已向用户授予在[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)调用中请求的访问权限。 如果是，则打开句柄;否则，调用会失败，并拒绝访问错误 \_ 。

打开句柄后，应用程序可以直接将命令发送到设备，这通常是通过使用 IOCTL 来完成的。 例如，若要发送 SCSI 传递命令，应用程序可以通过直接使用**ioctl \_ scsi \_ pass \_ **或**ioctl \_ scsi \_ pass \_ \_ **。

-   **IOCTL \_磁盘 \_ 获取 \_ 分区 \_ 信息**只需读取访问权限。

-   **IOCTL \_通过直接的 SCSI \_ 直通 \_ **和**IOCTL \_ scsi \_ 直通 \_ \_ ** ，要求调用方已打开接口（由存储设备驱动程序提供）的句柄，以便进行读写访问。

不会检查 SCSI 传递请求中给定的命令描述符块（CDB）中的操作码，以确定是否需要读取、写入或同时读取和写入访问权限。 这就是为什么 Windows 总是要求打开设备的句柄进行传递请求的读取和写入，即使应用程序只是执行读取、写入或根本没有数据传输。

**IOCTL \_可以发送磁盘 \_ 验证**，而不考虑在[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)调用中请求的访问权限。 当 i/o 管理器收到 IOCTL 时，它将检查该 IOCTL 所需的访问权限，并将它们与**CreateFile**调用中授予调用方的访问权限进行比较。 如果存在匹配项，则将 IOCTL 发送到目标设备;否则，IOCTL 调用会因错误拒绝访问而失败 \_ 。

例如，如果调用方已打开了一个用于只读访问的句柄，如下所示。

-   **IOCTL \_\_ \_ ** \_ 由于需要读取和写入访问权限，SCSI PASS 失败并拒绝错误访问。

-   **IOCTL \_磁盘 \_ 获取 \_ 分区 \_ 信息**将发送到驱动程序堆栈，因为它只需要读取访问权限。

 

 




