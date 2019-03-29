---
title: Microsoft 热量扩展的特定于设备的方法
description: 若要支持的热量区域和温度传感器的更灵活的设计，Windows 支持扩展 ACPI 散热区域模型。
ms.assetid: A8D90493-EE4A-40EC-BE8D-54B1C9EE94AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c673d4aa026a61fb196f0b66d684a7d86893ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568120"
---
# <a name="device-specific-method-for-microsoft-thermal-extensions"></a>Microsoft 热量扩展的特定于设备的方法


若要支持的热量区域和温度传感器的更灵活的设计，Windows 支持扩展 ACPI 散热区域模型。 具体而言，Windows 对于每个热量区域支持的热量最小的中止值限制 (MTL)，还支持共享热量区域之间的温度传感器。

有关 MTL 的详细信息，请参阅上标题为"在 Windows 的热量管理"的文档[Microsoft Connect 网站](http://connect.microsoft.com/site1304/Downloads/DownloadDetails.aspx?DownloadID=48106)。

若要使用这些功能，Oem 可以包括以下特定于设备的方法 (\_DSM) 任何热量区域的命名空间中。

## <a name="function-1-minimum-throttle-limit"></a>函数 1:最小的中止值


\_DSM 控件方法参数的热量最小控制器限制如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
-   **Arg1:** 修订 ID = 0
-   **Arg2:** 函数索引 = 1
-   **Arg3:**（未使用） 的空包

### <a name="return"></a>返回

一个整数值与当前的最小控制器限制，以百分比表示。 Windows 不会设置控制器限制低于此值。
## <a name="function-2-temperature-sensor-device"></a>函数 2:温度传感器设备


\_DSM 温度传感器设备的控制方法参数如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
-   **Arg1:** 修订 ID = 0
-   **Arg2:** 函数索引 = 2
-   **Arg3:**（未使用） 的空包

### <a name="return"></a>返回

对将返回此热量区域温度的设备的引用。
## <a name="temperature-sensor-device-dependency-requirement"></a>温度传感器设备依赖关系要求


如果通过报告温度传感器设备\_DSM 函数索引为 2，散热区域是另外需要包括\_DEP 对象，用于标识散热区域温度传感器设备上的依赖关系。

**请注意**  函数索引为 0 的每个\_DSM 是返回集支持的函数的索引，并始终是必需的查询函数。 有关详细信息，请参阅部分 9.14.1，"\_DSM （设备特定的方法）"，ACPI 5.0 规范。

 

 

 




