---
title: 选项文件示例
description: 选项文件示例
keywords:
- 选项文件 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f7816cee14379fd0b55b064b12d1a88ba3e690
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840791"
---
# <a name="option-file-examples"></a>选项文件示例

## <a name="example-1-change-the-timeout-value"></a>示例1：更改超时值

在以下示例 Sdv-default.xml 文件中，超时值将增加到两小时 (，即7200秒) 。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">7200</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads></SlamConfig>
```

## <a name="example-2-change-the-spaceout-value"></a>示例2：更改 Spaceout 值

在以下示例 Sdv-default.xml 文件中，可用于 SDV 的虚拟内存将增加到 3500 MB (3.5 GB) 。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">3500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads>
</SlamConfig>
```

## <a name="example-3-change-the-numberofthreads-value"></a>示例3：更改 NumberOfThreads 值

在下面的示例 Sdv-default.xml 文件中，SDV 的可用线程数限制为2。

```XML
<?xml version="1.0" encoding="utf-8" ?>
- <SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">2</SDV_SlamConfig_NumberOfThreads>
  </SlamConfig>
```
