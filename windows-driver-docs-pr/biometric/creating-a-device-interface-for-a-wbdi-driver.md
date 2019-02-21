---
title: 为 WBDI 驱动程序创建设备接口
description: 为 WBDI 驱动程序创建设备接口
ms.assetid: 8595092c-9105-4638-814a-74cdfa372638
keywords:
- 生物识别驱动程序 WDK，设备接口
- 设备接口 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f67ae29b232a0d3f688a3e347badfd6bb40aec01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541868"
---
# <a name="creating-a-device-interface-for-a-wbdi-driver"></a>为 WBDI 驱动程序创建设备接口


初始化设备回调对象并将其返回到该驱动程序，在队列设置的时间后，驱动程序应创建生物识别设备的设备接口实例。

具体而言，WBDI 驱动程序必须公开 GUID\_DEVINTERFACE\_生物识别\_读取器设备接口通过调用[ **IWDFDevice::CreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff557016):

```cpp
hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_BIOMETRIC_READER, NULL);
```

此调用对的调用后面[ **IWDFDevice::AssignDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff557006):

```cpp
hr = m_FxDevice->AssignDeviceInterfaceState(&GUID_DEVINTERFACE_BIOMETRIC_READER,
 NULL,
 TRUE);
```

想要向旧版 (非 WBDI) 生物识别堆栈公开功能的 WBDI 驱动程序应显示旧版应用程序的另一个设备接口，并确保独占值设置为零，将旧堆栈安装在 INX 文件中。

公开 GUID\_DEVINTERFACE\_生物识别\_读取器设备接口会导致 WBF 服务枚举的驱动程序。 如果未设置排他模式，WBF 不会尝试打开并控制设备。

或者，驱动程序无法检测到在内部，它处于旧模式，然后不公开 GUID\_DEVINTERFACE\_生物识别\_读取器设备接口。

 

 





