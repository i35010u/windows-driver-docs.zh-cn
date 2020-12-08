---
title: 从显示驱动程序调用 COPP DDI
description: 从显示驱动程序调用 COPP DDI
keywords:
- 调用 COPP DDI WDK DirectX VA
- COPP WDK DirectX VA，从显示器驱动程序调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e897d1f4418a039e783c3ec42ae952cdded24fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810389"
---
# <a name="calling-the-copp-ddi-from-the-display-driver"></a>从显示驱动程序调用 COPP DDI


## <span id="ddk_calling_the_copp_ddi_from_the_display_driver_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_THE_DISPLAY_DRIVER_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

显示驱动程序通过使用 COPP i/o 控件 (IOCTL) 请求，启动对视频微型端口驱动程序的 [COPP DDI](sample-functions-for-copp.md) 的调用。 显示驱动程序通过使用 COPP IOCTL 将同步 COPP 请求发送到视频微型端口驱动程序来调用 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) 函数。 图形设备接口 (GDI) 对输入和输出使用单个缓冲区来将请求传递到 i/o 子系统。 I/o 子系统将请求路由到视频端口，此端口使用视频微型端口驱动程序处理请求。

下面的示例数据结构和 IOCTLs 可用于在显示器驱动程序和视频微型端口驱动程序之间传输 COPP 信息。 根据需要，驱动程序可以使用数据结构和 IOCTLs 或创建新的结构。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;

#define IOCTL_COPP_OpenDevice \
        CTL_CODE(FILE_DEVICE_VIDEO, 2190, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_CloseDevice \
        CTL_CODE(FILE_DEVICE_VIDEO, 2191, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_GetCertificateLength \
        CTL_CODE(FILE_DEVICE_VIDEO, 2192, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_KeyExchange \
        CTL_CODE(FILE_DEVICE_VIDEO, 2193, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_StartSequence \
        CTL_CODE(FILE_DEVICE_VIDEO, 2194, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_Command \
        CTL_CODE(FILE_DEVICE_VIDEO, 2195, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_Status \
        CTL_CODE(FILE_DEVICE_VIDEO, 2196, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

如果未使用上述 IOCTLs，则可以定义自己的专用 IOCTLs，这必须按 [定义 I/o 控制代码](../kernel/defining-i-o-control-codes.md)中所述进行格式设置。

 

