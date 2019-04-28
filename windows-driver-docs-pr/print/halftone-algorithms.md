---
title: 半色调算法
description: 半色调算法
ms.assetid: 1831f952-4c83-4dfa-87e7-1c755f143227
keywords:
- HP/2 单色 WDK Unidrv，半色调算法
- PCL 5e WDK Unidrv，半色调算法
- 半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34703f5a3b5fc1bdbc8181c0c0ea413ede686d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341309"
---
# <a name="halftone-algorithms"></a>半色调算法





某些打印机供应商更喜欢打印不同类型的对象，如文本、 矢量对象和位图时使用不同的半色调算法。 下面的三个示例显示出应添加到 GPD 打印每个对象的类型。

第一个示例演示如何将合并半色调打印文本时的呈现。

```cpp
*Ifdef: WINNT_51
*Feature: TEXTHALFTONE
{
  *rcNameID: =TEXTHALFTONE_DISPLAY
  *DefaultOption: DETAIL
  *Option: DETAIL
   {
     *rcNameID: =DETAIL_HT_DISPLAY
     *Command: CmdSetTextHTAlgo { *Cmd : "<1B>*t0J" }
   }
  *Option: SMOOTH
   {
     *rcNameID: =SMOOTH_HT_DISPLAY
     *Name: "Smooth"
     *Command: CmdSetTextHTAlgo { *Cmd : "<1B>*t15J" }
   }
  *Option: BASIC
   {
     *rcNameID: =BASIC_HT_DISPLAY
     *Command: CmdSetTextHTAlgo { *Cmd : "<1B>*t18J" }
   }
}
*Endif:
```

第二个示例包括用于半色调打印矢量图形时呈现命令。

```cpp
*Ifdef:  WINNT_51
*Feature: GRAPHICSHALFTONE
{
  *rcNameID: =GRAPHICSHALFTONE_DISPLAY
  *DefaultOption: SMOOTH
  *Option: DETAIL
   {
     *rcNameID: =DETAIL_HT_DISPLAY
     *Command: CmdSetGraphicsHTAlgo { *Cmd : "<1B>*t15J" }
   }
  *Option: SMOOTH
   {
     *rcNameID: =SMOOTH_HT_DISPLAY
     *Command: CmdSetGraphicsHTAlgo { *Cmd : "<1B>*t18J" }
   }
  *Option: BASIC
   {
     *rcNameID: =BASIC_HT_DISPLAY
     *Command: CmdSetGraphicsHTAlgo { *Cmd : "<1B>*t18J" }
   }
}
*Endif:
```

第三个示例包括用于半色调打印位图时呈现命令。

```cpp
*Ifdef: WINNT_51
*Feature: PHOTOHALFTONE
{
  *rcNameID: =PHOTOHALFTONE_DISPLAY
  *DefaultOption: SMOOTH
  *Option: DETAIL
   {
     *rcNameID: =DETAIL_HT_DISPLAY
     *Command: CmdSetPhotoHTAlgo { *Cmd : "<1B>*t15J" }
   }
  *Option: SMOOTH
   {
     *rcNameID: =SMOOTH_HT_DISPLAY
     *Command: CmdSetPhotoHTAlgo { *Cmd : "<1B>*t7J" }
   }
  *Option: BASIC
   {
     *rcNameID: =BASIC_HT_DISPLAY
     *Command: CmdSetPhotoHTAlgo { *Cmd : "<1B>*t3J" }
   }
}
*Endif:
```

 

 




