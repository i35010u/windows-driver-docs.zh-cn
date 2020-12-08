---
title: 半色调算法
description: 半色调算法
keywords:
- HP-GL/2 单色 WDK Unidrv，半色调算法
- PCL-5e WDK Unidrv，半色调算法
- 半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad34be86c1fd7967a6274db7fd9603d4f00f24a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796873"
---
# <a name="halftone-algorithms"></a>半色调算法





某些打印机供应商喜欢在打印不同类型的对象（如文本、矢量对象和位图）时使用不同的半色调算法。 下面的三个示例显示了应添加到 GPD 的内容，以打印每种类型的对象。

第一个示例演示如何在打印文本时合并半色调呈现。

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

第二个示例包含打印矢量图形时半色调呈现的命令。

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

第三个示例包含打印位图时半色调呈现的命令。

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

 

 




