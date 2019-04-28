---
title: 控制设备访问权限
description: 控制设备访问权限
ms.assetid: E4FF73B3-87D0-458E-A042-E5A8F3DB1677
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6a8c24d0b41308fe5fec4f530ec04ac382ce89b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337853"
---
# <a name="controlling-device-access"></a>控制设备访问权限


UMDF 驱动程序主机进程在本地服务帐户的上下文中运行。 您的驱动程序可能需要访问其他设备或不允许组件通用化本地服务帐户的访问权限。

操作系统从 Windows 8 中，包括标识 UMDF 驱动程序的安全标识符 (SID)。 通过在其设备的安全要求中包括此 SID，设备或组件可以允许访问 UMDF 驱动程序同时阻止与其他请求来自本地服务帐户的访问权限。

UMDF 驱动程序的 SID 是 SDDL\_用户\_模式\_驱动程序和定义是 sddl.h 中。 此 SID 的完整表示形式是：

```cpp
S-1-5-84-0-0-0-0-0
```

此 SID 的缩写形式是 UD。 可在 Windows 8 中启动此缩写。

其 INF 文件中或在驱动程序中创建设备对象之前的驱动程序属于 UMDF 驱动程序可以指定 SID。

## <a name="specifying-device-security-in-an-inf-file"></a>INF 文件中指定设备安全


在 INF 文件中，您可以使用缩写的形式或完全指定的窗体的 SID。

缩写的形式是从 Windows 8 开始，提供：

```cpp
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;UD)"   
```

上的操作系统早于 Windows 8 中，您必须使用完全指定的窗体：

```cpp
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;S-1-5-84-0-0-0-0-0)"       
```

## <a name="specifying-device-security-in-a-kmdf-driver"></a>KMDF 驱动程序中指定设备安全


若要指定驱动程序中的安全要求，必须使用简写的形式，仅可在 Windows 8 中启动。 例如，KMDF 驱动程序可以通过访问其设备 UMDF 驱动程序使用以下方法：

```cpp
RtlInitUnicodeString(&sddlString, L"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;UD)");
status = WdfDeviceInitAssignSDDLString(DeviceInit, &sddlString);
```

 

 





