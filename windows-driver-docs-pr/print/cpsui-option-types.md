---
title: CPSUI 选项类型
description: CPSUI 选项类型
ms.assetid: 3b3c002c-a201-4f81-b208-30864343409b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd038401eb28da4d08094a230edda8ad8aadbe9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843064"
---
# <a name="cpsui-option-types"></a>CPSUI 选项类型


## <span id="ddk_cpsui_option_types_gg"></span><span id="DDK_CPSUI_OPTION_TYPES_GG"></span>


使用 CPSUI 创建属性表页时，必须使用[CPSUI 支持的窗口控件](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-supported-window-controls)定义用户可选择的选项。 这些控件由以下 CPSUI 选项类型标识：

[**TVOT\_2STATES**](tvot-2states.md)

[**TVOT\_3STATES**](tvot-3states.md)

[**TVOT\_CHKBOX**](tvot-chkbox.md)

[**TVOT\_COMBOBOX**](tvot-combobox.md)

[**TVOT\_"编辑框**](tvot-editbox.md)

[**TVOT\_LISTBOX**](tvot-listbox.md)

[**TVOT\_按键**](tvot-pushbutton.md)

[**TVOT\_滚动条**](tvot-scrollbar.md)

[**TVOT\_跟踪条**](tvot-trackbar.md)

[**TVOT\_UDARROW**](tvot-udarrow.md)

选项的类型是在[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)结构的**类型**成员中指定的。

 

 




