---
title: 控制设备访问权限
description: 控制设备访问权限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bf9cc283191679089c1c20a77a43dbcd5994f04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829073"
---
# <a name="controlling-device-access"></a>控制设备访问权限


UMDF 驱动程序主机进程在本地服务帐户的上下文中运行。 你的驱动程序可能需要访问不允许通用化访问本地服务帐户的其他设备或组件。

从 Windows 8 开始，操作系统包含一个安全标识符 (SID) ，用于标识 UMDF 驱动程序。 通过在其设备安全要求中包含此 SID，设备或组件可以允许访问 UMDF 驱动程序，同时阻止来自本地服务帐户的其他请求的访问。

UMDF 驱动程序的 SID 为 SDDL \_ 用户 \_ 模式 \_ 驱动程序，并且该定义位于 sddl. h 中。 此 SID 的完整表示形式为：

```cpp
S-1-5-84-0-0-0-0-0
```

此 SID 的缩写为 UD。 此缩写在 Windows 8 中开始可用。

UMDF 驱动程序的外部驱动程序可以在创建设备对象之前，在其 INF 文件或驱动程序中指定该 SID。

## <a name="specifying-device-security-in-an-inf-file"></a>在 INF 文件中指定设备安全性


在 INF 文件中，可以使用缩写形式或完全指定的 SID 形式。

从 Windows 8 开始可以使用缩写形式：

```cpp
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;UD)"   
```

在 Windows 8 之前的操作系统上，必须使用完全指定的格式：

```cpp
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;S-1-5-84-0-0-0-0-0)"       
```

## <a name="specifying-device-security-in-a-kmdf-driver"></a>在 KMDF 驱动程序中指定设备安全性


若要在驱动程序中指定安全要求，必须使用缩写形式，该格式仅在 Windows 8 中开始使用。 例如，KMDF 驱动程序可以通过使用以下内容，从 UMDF 驱动程序启用对其设备的访问：

```cpp
RtlInitUnicodeString(&sddlString, L"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;UD)");
status = WdfDeviceInitAssignSDDLString(DeviceInit, &sddlString);
```

 

 





