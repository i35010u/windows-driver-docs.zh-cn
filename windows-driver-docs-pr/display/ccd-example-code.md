---
title: CCD 示例伪代码
description: 使用 CCD Api 设置克隆视图的示例伪代码
keywords:
- 连接显示 WDK Windows 7 显示，CCD Api，示例代码
- 连接显示 WDK Windows Server 2008 R2 display、CCD Api、示例代码
- 配置显示 WDK Windows 7 显示、CCD Api、示例代码
- 配置显示 WDK Windows Server 2008 R2 display、CCD Api、示例代码
- CCD Api WDK Windows 7 显示，示例代码
- CCD Api WDK Windows Server 2008 R2 显示，示例代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d8588abc792a16be9876e86355e3e2346bda52
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810351"
---
# <a name="ccd-example-pseudocode"></a>CCD 示例伪代码

本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

下面的伪代码演示了如何使用 (CCD) Api 的连接和配置显示来设置克隆视图：

```cpp
SetCloneView
{
    // Determine the size of the path and mode information arrays needed
    // to hold all valid paths by calling GetDisplayConfigBufferSizes
    // with flags=QDC_ALL_PATHS

    // Using the returned numPathArrayElements and numModeInfoArrayElements,
    // allocate memory for the path and mode information arrays as follows:
    // pathArray size is numPathArrayElements*sizeof(DISPLAYCONFIG_PATH_INFO)
    // modeInfoArray size is numModeInfoArrayElements*sizeof(DISPLAYCONFIG_MODE_INFO)

    // Obtain the path and mode information for all possible paths by
    // calling QueryDisplayConfig with flags=QDC_ALL_PATHS and pointers
    // to the allocated path and mode info arrays.

    // Find the primary path by searching the returned array of
    // DISPLAYCONFIG_PATH_INFO structs for an active path that is
    // located at desktop position (0, 0).

    // Determine the user friendly name of the current primary by
    // calling DisplayConfigGetDeviceInfo with a type of
    // DISPLAYCONFIG_DEVICE_INFO_GET_TARGET_NAME, and the
    // adapter ID and target ID from the DISPLAYCONFIG_PATH_TARGET_INFO
    // of the primary path.

    // DisplayConfigGetDeviceInfo can determine the user friendly names
    // for all of the paths that might be part of the clone.
    // Allow the user to pick which monitor the clone is enabled on.
    // Only provide the user options of the paths from the current primary
    // to targets with monitors that are connected or that are forceable.  
    // Store a newClonePath pointer to the DISPLAYCONFIG_PATH_INFO that
    // the user picked.

    // Mark the new clone path as active:
    // NewClonePath->flags |= DISPLAYCONFIG_PATH_ACTIVE;
    // NewClonePath->sourceInfo.modeInfoIdx = DISPLAYCONFIG_PATH_MODE_IDX_INVALID;
    // NewClonePath->targetInfo.modeInfoIdx = DISPLAYCONFIG_PATH_MODE_IDX_INVALID;

    // Set the new topology by calling SetDisplayConfig with flags =
    // (SDC_APPLY | SDC_SAVE_TO_DATABASE | SDC_ALLOW_CHANGES
    //  | SDC_USE_SUPPLIED_DISPLAY_CONFIG) to change to the clone topology.
}
```
