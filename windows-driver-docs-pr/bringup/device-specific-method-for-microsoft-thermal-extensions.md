---
title: Microsoft 热量扩展的特定于设备的方法
description: 为了支持更灵活的热区域和热传感器设计，Windows 支持向 ACPI 热区模型扩展。
ms.assetid: A8D90493-EE4A-40EC-BE8D-54B1C9EE94AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3373759f185d1e98149df9271d85869999c8a1e8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101526"
---
# <a name="device-specific-method-for-microsoft-thermal-extensions"></a>Microsoft 热量扩展的特定于设备的方法


为了支持更灵活的热区域和热传感器设计，Windows 支持向 ACPI 热区模型扩展。 具体而言，Windows 支持每个热量区域 (MTL) 的热量最小限制，还支持在热量区域之间共享温度传感器。

有关 MTL 的详细信息，请参阅 [Microsoft Connect 网站](/collaborate/connect-redirect?DownloadID=48106)上标题为 "Windows 中的热量管理" 的文档。

若要使用这些功能，Oem 可以 \_ 在任何热区的命名空间中 (DSM) 包含以下特定于设备的方法。

## <a name="function-1-minimum-throttle-limit"></a>函数1：最小限制限制


\_热量最小限制限制的 DSM 控制方法参数如下：

### <a name="arguments"></a>参数

-   **Arg0：** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
-   **Arg1：** 修订版 ID = 0
-   **Arg2：** 函数 index = 1
-   **Arg3：** 空包 (未使用) 

### <a name="return"></a>返回

一个整数值，它具有当前的最小限制限制（以百分比表示）。 Windows 不会将限制限制设置为低于此值。
## <a name="function-2-temperature-sensor-device"></a>函数2：温度传感器设备


\_温度传感器设备的 DSM 控制方法参数如下：

### <a name="arguments"></a>参数

-   **Arg0：** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
-   **Arg1：** 修订版 ID = 0
-   **Arg2：** 函数 index = 2
-   **Arg3：** 空包 (未使用) 

### <a name="return"></a>返回

对将返回此热区温度的设备的引用。
## <a name="temperature-sensor-device-dependency-requirement"></a>温度传感器设备依赖关系要求


如果温度传感器设备是通过 \_ DSM 函数索引2报告的，则该热区还需要包含一个用于 \_ 标识温度传感器设备上的热区依赖的 DEP 对象。

**注意**   每个 DSM 的函数索引 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关详细信息，请参阅 \_ ACPI 5.0 规范的 "DSM (设备特定方法) " 部分。

 

 

