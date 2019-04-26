---
title: 系统定义的 IOCTL_VIDEO_XXX 请求
description: 系统定义的 IOCTL_VIDEO_XXX 请求
ms.assetid: 30309de1-c991-402d-a701-7e88c3367d24
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，处理请求
- 请求处理 WDK 微型端口
- I/O WDK 微型端口
- 系统定义 IOCTL_VIDEO_XXX 请求 WDK 微型端口
- IOCTL_VIDEO_XXX 请求 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c5d7b214e6462ba929ac69f066ad1d8db51a2da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330593"
---
# <a name="system-defined-ioctlvideoxxx-requests"></a>系统定义 IOCTL\_视频\_XXX 请求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常情况下，大多数微型端口驱动程序支持以下请求：

[**IOCTL\_视频\_查询\_NUM\_利用\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff567824)

[**IOCTL\_视频\_查询\_利用\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff567816)

[**IOCTL\_视频\_查询\_当前\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff567819)

[**IOCTL\_视频\_设置\_当前\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff567846)

[**IOCTL\_VIDEO\_RESET\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff567834)

[**IOCTL\_视频\_地图\_视频\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff567812)

[**IOCTL\_视频\_UNMAP\_视频\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff568153)

[**IOCTL\_视频\_共享\_视频\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff568149)

[**IOCTL\_视频\_取消共享\_视频\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff568155)

[**IOCTL\_视频\_查询\_公共\_访问\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff567829)

[**IOCTL\_视频\_免费\_公共\_访问\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff567796)

[**IOCTL\_视频\_获取\_POWER\_管理**](https://msdn.microsoft.com/library/windows/hardware/ff567803)

[**IOCTL\_VIDEO\_SET\_POWER\_MANAGEMENT**](https://msdn.microsoft.com/library/windows/hardware/ff568148)

[**IOCTL\_VIDEO\_GET\_CHILD\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567801)

[**IOCTL\_VIDEO\_SET\_CHILD\_STATE\_CONFIGURATION**](https://msdn.microsoft.com/library/windows/hardware/ff567840)

[**IOCTL\_视频\_VALIDATE\_子\_状态\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff568156)

具体取决于适配器的功能，微型端口驱动程序可以支持以下额外的请求：

[**IOCTL\_视频\_查询\_颜色\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff567817)

[**IOCTL\_视频\_设置\_颜色\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff567842) （如果设备具有调色板为必需）

[**IOCTL\_视频\_禁用\_指针**](https://msdn.microsoft.com/library/windows/hardware/ff567786)

[**IOCTL\_VIDEO\_ENABLE\_POINTER**](https://msdn.microsoft.com/library/windows/hardware/ff567793)

[**IOCTL\_视频\_查询\_指针\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff567826)

[**IOCTL\_视频\_查询\_指针\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff567825)

[**IOCTL\_VIDEO\_SET\_POINTER\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff568144)

[**IOCTL\_视频\_查询\_指针\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff567827)

[**IOCTL\_视频\_设置\_指针\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff568145)

[**IOCTL\_VIDEO\_HANDLE\_VIDEOPARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567805)

[**IOCTL\_视频\_交换机\_双视图**](https://msdn.microsoft.com/library/windows/hardware/ff568151)

支持以下其他请求所需的 VGA 兼容的 SVGA 微型端口驱动程序：

[**IOCTL\_VIDEO\_SAVE\_HARDWARE\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567838)

[**IOCTL\_视频\_还原\_硬件\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567835)

[**IOCTL\_视频\_禁用\_游标**](https://msdn.microsoft.com/library/windows/hardware/ff567784)

[**IOCTL\_视频\_启用\_游标**](https://msdn.microsoft.com/library/windows/hardware/ff567788)

[**IOCTL\_视频\_查询\_光标\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff567820)

[**IOCTL\_视频\_设置\_光标\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff567847)

[**IOCTL\_视频\_查询\_光标\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff567821)

[**IOCTL\_视频\_设置\_光标\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff567849)

[**IOCTL\_VIDEO\_GET\_BANK\_SELECT\_CODE**](https://msdn.microsoft.com/library/windows/hardware/ff567799)

[**IOCTL\_视频\_设置\_调色板\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff568142)

[**IOCTL\_视频\_负载\_AND\_设置\_字体**](https://msdn.microsoft.com/library/windows/hardware/ff567809)

可以在找到每个 IOCTL 详细信息[视频微型端口驱动程序 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff570515)。 微型端口驱动程序编写人员不应使用未记录的系统定义 Ioctl。

 

 





