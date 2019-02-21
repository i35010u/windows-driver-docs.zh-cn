---
title: 从显示驱动程序调用 COPP DDI
description: 从显示驱动程序调用 COPP DDI
ms.assetid: d91d8a62-f212-4ae7-be61-b973d6495880
keywords:
- 调用 COPP DDI WDK DirectX VA
- COPP WDK DirectX VA，从显示驱动程序中调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fae21bc42e4183ae0e25605c9f9d917b044574d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555206"
---
# <a name="calling-the-copp-ddi-from-the-display-driver"></a>从显示驱动程序调用 COPP DDI


## <span id="ddk_calling_the_copp_ddi_from_the_display_driver_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_THE_DISPLAY_DRIVER_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

显示驱动程序将启动对视频的微型端口驱动程序的调用[COPP DDI](sample-functions-for-copp.md)通过使用 COPP I/O 控制 (IOCTL) 请求。 显示驱动程序调用[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)函数通过使用 COPP IOCTL 将同步的 COPP 请求发送到的微型端口驱动程序。 图形设备接口 (GDI) 使用输入和输出的单独缓冲区以将请求传递到 I/O 子系统。 I/O 子系统将请求路由到通过使用微型端口驱动程序处理请求的视频端口。

下面的示例数据结构和 Ioctl 可以用于显示驱动程序和视频的微型端口驱动程序之间传输 COPP 信息。 驱动程序可以是使用的数据结构和 Ioctl 或创建新的根据需要。

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

如果不使用前面 Ioctl，则可以定义中所述格式必须自己专用 Ioctl[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)。

 

 





