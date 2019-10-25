---
title: 使用 VideoPortGetProcAddress
description: 使用 VideoPortGetProcAddress
ms.assetid: 48dace7e-7ba3-48bf-9788-469ff42f6fe3
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、多个 Windows 版本、VideoPortGetProcAddress
- VideoPortGetProcAddress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c90318c70415fe2eddea702cfa9fcf5b4598d5fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829239"
---
# <a name="using-videoportgetprocaddress"></a>使用 VideoPortGetProcAddress


## <span id="ddk_using_videoportgetprocaddress_gg"></span><span id="DDK_USING_VIDEOPORTGETPROCADDRESS_GG"></span>


只要微型端口驱动程序不尝试使用特定于较新操作系统版本的功能，就可以在一个基于 NT 的操作系统版本上开发的视频微型端口驱动程序加载并运行。

加载视频微型端口驱动程序时，视频\_端口的**VideoPortGetProcAddress**成员[ **\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)结构包含视频端口驱动程序导出[**的回调例程的地址。VideoPortGetProcAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_port_get_proc_address)。 微型端口驱动程序可以使用此回调例程查找从*videoprt*导出的视频端口函数的地址。 当微型端口驱动程序具有此函数的地址后，它可以使用此地址调用函数。 下面的示例代码对此进行了演示。

```cpp
  // Useful typedef for a function pointer type
  //   that points to a function with same argument types
  //   as VideoPortCreateSecondaryDisplay
typedef VP_STATUS ( *pFunc(PVOID, PVOID *, ULONG));

  // Declare a pointer to a function
pFunc pVPFunction;

  // Declare a pointer to a VIDEO_PORT_CONFIG_INFO struct
PVIDEO_PORT_CONFIG_INFO pConfigInfo;

  // Call through VideoPortGetProcAddress callback
  //   to get address of VideoPortCreateSecondaryDisplay
pVPFunction = (pFunc)
  ( *(pConfigInfo->VideoPortGetProcAddress)(
                        pDeviceExt, 
                       "VideoPortCreateSecondaryDisplay")
  );
if (NULL == pVPFunction) {
  // Video port does not export the function
  ...
}
else {
  Status = pVPFunction(DevExtension, 
                      &SecondDevExtension,
                       VIDEO_DUALVIEW_REMOVABLE);
} 
```

执行完*VideoPortGetProcAddress*回调例程的调用后， *pVPFunction*为**NULL**或包含**VideoPortCreateSecondaryDisplay**函数的地址。 如果*pVPFunction*为**NULL**，则视频端口驱动程序不会导出你要查找的函数，并且微型端口驱动程序不得尝试使用它。 如果*pVPFunction*不为**NULL**，则可以使用此指针调用**VideoPortCreateSecondaryDisplay** ，如前面的示例中所示。

 

 





