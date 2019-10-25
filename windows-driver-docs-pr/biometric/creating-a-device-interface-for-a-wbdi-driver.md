---
title: 为 WBDI 驱动程序创建设备接口
description: 为 WBDI 驱动程序创建设备接口
ms.assetid: 8595092c-9105-4638-814a-74cdfa372638
keywords:
- 生物识别驱动程序 WDK，设备接口
- 设备接口 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02981a59046637324eb6e9b7823d6031ce759305
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833950"
---
# <a name="creating-a-device-interface-for-a-wbdi-driver"></a>为 WBDI 驱动程序创建设备接口


在将设备回调对象初始化并返回给驱动程序之后，在安装队列时，驱动程序应为该生物识别设备创建一个设备接口实例。

具体而言，WBDI 驱动程序必须通过调用[**IWDFDevice：： CreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)\_生物识别\_读取器设备接口公开 GUID\_DEVINTERFACE：

```cpp
hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_BIOMETRIC_READER, NULL);
```

此调用后跟对[**IWDFDevice：： AssignDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)的调用：

```cpp
hr = m_FxDevice->AssignDeviceInterfaceState(&GUID_DEVINTERFACE_BIOMETRIC_READER,
 NULL,
 TRUE);
```

要向传统（非 WBDI）生物识别堆栈公开功能的 WBDI 驱动程序应为旧版应用程序公开另一设备接口，并确保在安装旧版堆栈的 INX 文件中将独占值设置为零。

公开 GUID\_DEVINTERFACE\_生物识别\_读取器设备接口会导致 WBF 服务仅枚举驱动程序。 如果未设置专用模式，则 WBF 不会尝试打开和控制设备。

或者，驱动程序可以在内部检测到它处于旧模式，然后不\_DEVINTERFACE\_生物识别\_读取器设备接口公开 GUID。

 

 





