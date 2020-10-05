---
title: 实现无人参与 Windows 安装程序设置
description: 本主题介绍如何设置无人参与的 Windows 安装程序组件设置。
ms.assetid: 593F8E05-F886-45FE-83EB-8DDD204F7900
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 47571b964c5f221bb1af499bf818e4de26ecded3
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734075"
---
# <a name="implement-the-unattended-windows-setup-setting"></a>实现无人参与 Windows 安装程序设置


本主题介绍如何设置无人参与的 Windows 安装程序组件设置。

强烈建议使用 [Windows 系统映像管理器](/previous-versions/windows/it-pro/windows-vista/cc722301(v=ws.10)) 编辑 Windows 安装程序的无人参与文件。

下面是一个示例输出文件：

``` syntax
<unattend xmlns="urn:schemas-microsoft-com:unattend">
  <settings pass="specialize">
    <component
        name="Microsoft-Windows-GPIOButtons"
        processorArchitecture="x86"> <!-- ... Additional component attributes-->
      <ConvertibleSlateMode>1</ConvertibleSlateMode> <!-- Values: {0 (slate); 1 (laptop)}-->
    </component>
  </settings>
</unattend>
```

 

