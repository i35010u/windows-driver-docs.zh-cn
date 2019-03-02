---
title: 驱动程序包元数据
description: 介绍合作伙伴中心提交的驱动程序包元数据的结构。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: e3f4022d4715fc8d76b3c749df74db56ba5cf4d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518256"
---
# <a name="driver-package-metadata"></a>驱动程序包元数据

驱动程序元数据包是与提交关联的文件。 元数据包包含有关驱动程序包或捆绑包中每个 INF 文件的详细信息。 可以使用[获取提交](get-a-submission.md)方法下载此文件。 此文件在提交的[链接对象](get-product-data.md#link-object)中通过 rel - driverMetadata 提供。 

## <a name="driver-metadata-structure"></a>驱动程序元数据结构

```json
{
  "BundleInfoMap": {
    "dc3b111e-c750-4a55-96ce-0eae1d1da8a2": {
      "Locales": [
        "English"
      ],
      "InfInfoMap": {
        "foo_bar.inf": {
          "DriverPackageFamilyId": "RAID-foo_bar.inf",
          "InfClass": "SCSIAdapter",
          "DriverVersion": "1.1.1.1",
          "DriverDate": "2018-01-11T00:00:00",
          "ExtensionId": null,
          "Provider": "RAID",
          "ClassGuid": "{a43418dc-cfc9-42e1-85b0-2d644331e214}",
          "InstallationComputerHardwareIds": [
            "a9a8e6fc-4969-4336-927c-9d8f7b6c1d14",
            "a4a127cb-2c10-464e-abb5-e78fcdf0d3c3"
          ],
          "OSPnPInfoMap": {
            "WINDOWS_v100_RS3_FULL": {
              "pci\\ven_test&dev_abcd": {
                "Manufacturer": "RAID",
                "DeviceDescription": "Virtual Raid Adapter",
                "FeatureScore": null
              }
            }
          }
        }
      }
    }
  }
}
```

此文件具有以下值：

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
|BundleInfoMap|对象|这是父级。 它由 GUID 标识，并包含有关驱动程序捆绑包的所有详细信息。 此值映射到[硬件 ID 对象](get-shipping-labels.md#hardware-id-object)中的 *bundleID*|
|区域设置|字符串数组|捆绑包的适用区域设置数组|
|InfInfoMap|对象数组|描述捆绑包中每个 INF 文件的数组。 每个项的标识符是 INF 文件名。 INF 名称映射到[硬件 ID 对象](get-shipping-labels.md#hardware-id-object)中的 *infID*。|
|DriverPackageFamilyId|字符串|驱动程序包系列的 ID|
|InfClass|字符串|驱动程序的设备类或 INF 类|
|DriverVersion|字符串|驱动程序的版本|
|DriverDate|日期/时间|此驱动程序的日期和时间|
|ExtensionId|GUID|适用于扩展 INF。 表示此 INF 的扩展 ID 的 GUID|
|提供程序|字符串|此驱动程序的提供程序|
|ClassGuid|字符串|驱动程序的类 GUID|
|InstallationComputerHardwareIds|GUID 数组|此驱动程序可以针对的 CHID 列表|
|OSPnPInfoMap|对象数组|将操作系统映射到硬件 ID 的对象数组。 对象有一个基元素，即操作系统。 每个操作系统内部都有一个 PNP 或硬件 ID 以及详细信息的列表。 操作系统映射到[硬件 ID 对象](get-shipping-labels.md#hardware-id-object)中的 operatingSystemCode，硬件 ID 映射到 *pnpString*|
|制造商|字符串|硬件 ID 的制造商|
|DeviceDescription|字符串|硬件 ID 的说明|
|FeatureScore|字符串|驱动程序的功能评分|

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
