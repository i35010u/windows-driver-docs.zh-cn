---
title: 使用 VideoPortGetProcAddress
description: 使用 VideoPortGetProcAddress
ms.assetid: 48dace7e-7ba3-48bf-9788-469ff42f6fe3
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，多个 Windows 版本中 VideoPortGetProcAddress
- VideoPortGetProcAddress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707c39b096c8faa1d88c610310f86de5224ca8c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373561"
---
# <a name="using-videoportgetprocaddress"></a>使用 VideoPortGetProcAddress


## <span id="ddk_using_videoportgetprocaddress_gg"></span><span id="DDK_USING_VIDEOPORTGETPROCADDRESS_GG"></span>


微型端口驱动程序开发一个可以加载和运行较早的操作系统版本，在基于 NT 的操作系统版本上，只要微型端口驱动程序不会尝试使用特定于较新的操作系统版本的功能。

微型端口驱动程序加载时， **VideoPortGetProcAddress**的成员[**视频\_端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)结构包含的地址的视频端口驱动程序导出的回调例程[ **VideoPortGetProcAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_port_get_proc_address)。 微型端口驱动程序可以使用此回调例程来查找从导出的视频端口函数的地址*videoprt.sys*。 微型端口驱动程序具有函数的地址后，它可以使用此地址调用该函数。 下面的示例代码所示。

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

通过在调用后*VideoPortGetProcAddress*已执行的回调例程*pVPFunction*任一项**NULL**或包含的地址**VideoPortCreateSecondaryDisplay**函数。 如果*pVPFunction*是**NULL**、 视频端口驱动程序不会导出要查找，该函数和微型端口驱动程序必须不尝试使用它。 如果*pVPFunction*不是**NULL**，可以使用此指针来调用**VideoPortCreateSecondaryDisplay**中前面的示例中所示。

 

 





