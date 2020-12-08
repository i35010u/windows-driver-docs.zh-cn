---
title: 为 WBDI 驱动程序创建设备接口
description: 为 WBDI 驱动程序创建设备接口
keywords:
- 生物识别驱动程序 WDK，设备接口
- 设备接口 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4e7dc7eb448b51375638faee3a5879a39e6193
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784299"
---
# <a name="creating-a-device-interface-for-a-wbdi-driver"></a>为 WBDI 驱动程序创建设备接口


在将设备回调对象初始化并返回给驱动程序之后，在安装队列时，驱动程序应为该生物识别设备创建一个设备接口实例。

具体而言，WBDI 驱动程序必须 \_ \_ \_ 通过调用 [**IWDFDevice：： CreateDeviceInterface**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)来公开 GUID DEVINTERFACE 生物识别读取器设备接口：

```cpp
hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_BIOMETRIC_READER, NULL);
```

此调用后跟对 [**IWDFDevice：： AssignDeviceInterfaceState**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)的调用：

```cpp
hr = m_FxDevice->AssignDeviceInterfaceState(&GUID_DEVINTERFACE_BIOMETRIC_READER,
 NULL,
 TRUE);
```

要向旧的 (非 WBDI) 生物识别堆栈公开功能的 WBDI 驱动程序应为旧版应用程序公开另一个设备接口，并确保在安装旧版堆栈的 INX 文件中将独占值设置为零。

公开 GUID \_ DEVINTERFACE \_ 生物识别 \_ 读卡器设备接口会导致 WBF 服务仅枚举驱动程序。 如果未设置专用模式，则 WBF 不会尝试打开和控制设备。

或者，驱动程序可以在内部检测到它处于传统模式，然后不公开 GUID \_ DEVINTERFACE \_ 生物识别 \_ 读取器设备接口。

 

