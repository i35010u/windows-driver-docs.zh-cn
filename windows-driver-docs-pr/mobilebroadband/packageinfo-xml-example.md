---
title: PackageInfo XML 示例
description: PackageInfo XML 示例
ms.assetid: 4e514e79-d450-4cae-a40d-16ce86f95e43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3eb1ab27d978d8eaa79d9fdcfe7ad1b24637d2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541077"
---
# <a name="packageinfo-xml-example"></a>PackageInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

下面的 XML 文档使用[PackageInfo XML 架构](packageinfo-xml-schema.md)指定供应商的元数据包的组件。

该程序包适用于具有以下硬件 ID 的服务：

MBAE:0:L9@E}}DT2.\*F65MQA57Y+L

**请注意**   PackageInfo.xml 中包含的硬件 Id 都必须具有"DOID:"前缀添加到它们。

 

包也是 EN-US 区域设置，其中该文档将设置为元数据包的组件的默认区域设置。

``` syntax
<?xml version="1.0" encoding ="UTF-8" ?>

  <PackageInfo xmlns=http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11/
               xmlns:v2=” http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2”>

  <MetadataKey>
      <HardwareIDList>
        <HardwareID>DOID:MBAE:0:L9@E}}DT2.*F65MQA57Y+L</HardwareID>
      </HardwareIDList>
      <Locale default="true">EN-US</Locale>
      <LastModifiedDate>2008-01-24T00:00:00Z</LastModifiedDate>
      <v2:MultipleLocale>true</v2:MultipleLocale>
  </MetadataKey>

  <PackageStructure>
      <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
      <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/ServiceInfo/2007/11/">ServiceInformation</Metadata>
      <Metadata MetadataID=”http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/”>WindowsInformation</Metadata>
    </PackageStructure>
</PackageInfo>
```

 

 





