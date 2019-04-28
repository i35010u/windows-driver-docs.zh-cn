---
title: PropVariant 帮助程序
description: 用于操作与传感器相关联的 PROPVARIANT 结构 v2 传感器驱动程序使用 PropVariant 帮助器函数。
ms.assetid: 5A5A008A-399F-4464-ADD0-7F2DDACB6D4B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb19c657d5e56b4459081b6645c3d48f4af60728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330070"
---
# <a name="propvariant-helpers"></a>PropVariant 帮助程序


PropVariant 帮助器函数用于处理由 v2 传感器驱动程序[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)与传感器相关联的结构。

传感器设备驱动程序软件接口 (DDSI) 一起使用的帮助器函数。

**InitPropVariantFromFloat**

通过传感器 DDSI 的使用情况

-   初始化[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)结构。

备注

-   此函数接收浮点数，然后根据该变量，它会创建并初始化[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)结构。

**PropKeyFindKeyGetPropVariant**

通过传感器 DDSI 的使用情况

-   检索[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)结构。

备注

-   无。

**PropKeyFindKeySetPropVariant**

通过传感器 DDSI 的使用情况

-   集[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)结构。

备注

-   无。

**PropKeyFindKeyGetFileTime**

通过传感器 DDSI 的使用情况

-   检索与数据文件相关联的时间戳。

备注

-   这是*filetime*的成员[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)与提供的属性键匹配的结构。

**PropKeyFindKeyGetGuid**

通过传感器 DDSI 的使用情况

-   检索传感器的 GUID。

备注

-   这是*puuid*的成员[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)与提供的属性键匹配的结构。

**PropKeyFindKeyGetBool**

通过传感器 DDSI 的使用情况

-   检索一个 BOOL 值从[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetUlong**

通过传感器 DDSI 的使用情况

-   检索 ULONG 取值[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetUshort**

通过传感器 DDSI 的使用情况

-   检索 USHORT 取值[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetFloat**

通过传感器 DDSI 的使用情况

-   检索一个浮点值，从[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetDouble**

通过传感器 DDSI 的使用情况

-   检索一个双精度值从[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetInt32**

通过传感器 DDSI 的使用情况

-   检索一个 32 位的值从[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetInt64**

通过传感器 DDSI 的使用情况

-   检索一个 64 位的值从[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropKeyFindKeyGetNthUlong**

通过传感器 DDSI 的使用情况

-   检索第 n 个 ULONG 取值[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)根据提供的属性的键的集合列表中。

备注

-   无。

**PropKeyFindKeyGetNthUshort**

通过传感器 DDSI 的使用情况

-   检索第 n 个 UShort 取值[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)根据提供的属性的键的集合列表中。

备注

-   无。

**PropKeyFindKeyGetNthInt64**

通过传感器 DDSI 的使用情况

-   检索中的第 n 个 Int64 值[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)根据提供的属性的键的集合列表中。

备注

-   无。

**IsKeyPresentInPropertyList**

通过传感器 DDSI 的使用情况

-   返回一个布尔值。

备注

-   布尔值指示是否中找到属性键[**传感器\_属性\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)传感器与关联的结构。

**IsKeyPresentInCollectionList**

通过传感器 DDSI 的使用情况

-   返回一个布尔值。

备注

-   布尔值指示是否中找到属性键[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。 与传感器相关联。

**IsCollectionListSame**

通过传感器 DDSI 的使用情况

-   返回一个布尔值。

备注

-   比较两个[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构以确定它们是否相同。

**PropVariantGetInformation**

通过传感器 DDSI 的使用情况

-   检索有关大小、 偏移量和其他信息[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)传感器与关联的结构。

备注

-   无。

**PropertiesListCopy**

通过传感器 DDSI 的使用情况

-   副本的源属性列表中的信息复制到一个目标。

备注

-   请参阅[**传感器\_属性\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)有关详细信息。

**PropertiesListGetFillableCount**

通过传感器 DDSI 的使用情况

-   返回特定大小的缓冲区可能是可以容纳的元素数目。

备注

-   无。

## <a name="requirements"></a>要求


|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>相关主题


[帮助器函数的封送处理](marshalling-helper-functions.md)

 

 






